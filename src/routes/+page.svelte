<script>
  // @ts-nocheck

  let prueba = "hola mundo";
  let resultado = "";
  let entrada1 = "";
  let entrada2 = "";
  let entrada3 = "";
  let entrada4 = "";
  let entrada5 = "";

  function predict(inputs, weight) {
    let neti = weight[0];
    for (let i = 0; i < inputs.length; i++) {
      neti += inputs[i] * weight[i + 1];
    }
    return neti >= 0 ? 1 : 0;
  }

  function evaluar() {
    resultado = predict([entrada1, entrada2, entrada3, entrada4, entrada5], weight);
  }

  function train(trainingData, weight) {
    let trained = false;
    let err;
    while (!trained) {
      trained = true;
      trainingData.forEach((data) => {
        const output = predict(data.x, weight);

        err = data.out - output;
        if (err != 0) {
          trained = false;
          weight = recalcular(err, weight, [1, ...data.x]);
        }
      });
    }
    return weight;
  }

  function recalcular(error, pesos, entrada) {
    let wOut = [];
    for (let i = 0; i < pesos.length; i++) {
      wOut.push(pesos[i] + error * entrada[i]);
    }
    return wOut;
  }

  const trainingData = [
    { x: [0, 0, 0, 0, 0], out: 0 },
    { x: [0, 0, 0, 0, 1], out: 0 },
    { x: [0, 0, 1, 0, 1], out: 0 },
    { x: [0, 0, 0, 1, 1], out: 0 },
    { x: [0, 0, 0, 1, 0], out: 0 },
    { x: [0, 0, 1, 1, 0], out: 0 },
    { x: [0, 1, 0, 1, 0], out: 0 },
    { x: [0, 1, 1, 0, 0], out: 0 },
    { x: [1, 1, 0, 0, 0], out: 0 },
    { x: [0, 0, 1, 1, 1], out: 1 },
    { x: [1, 0, 1, 0, 1], out: 1 },
    { x: [0, 1, 1, 1, 1], out: 1 },
    { x: [1, 0, 0, 1, 1], out: 1 },
    { x: [1, 1, 0, 1, 1], out: 1 },
    { x: [1, 1, 1, 0, 1], out: 1 },
    { x: [1, 1, 1, 0, 0], out: 1 },
    { x: [1, 1, 1, 1, 0], out: 1 },
    { x: [1, 1, 1, 1, 1], out: 1 },
   
  ];

  const weight = train(trainingData, [0.5, 1.5, 2, 0, 1, -0.5]);
  
</script>
<input bind:value={entrada1} type="number"/>
<input bind:value={entrada2} type="number"/>
<input bind:value={entrada3} type="number"/>
<input bind:value={entrada4} type="number"/>
<input bind:value={entrada5} type="number"/>
<h1>{resultado}</h1>

<button on:click={evaluar}>evaluar</button>
