<script>
  // Import components
  import FirstStart from './FirstStart.svelte';
  import Calculator from "./Calculator.svelte";
  import {fs} from "@tauri-apps/api";
  import {BaseDirectory} from "@tauri-apps/api/fs";

  let viewportComponent = null;
  const states = [FirstStart, Calculator];
  let currentState = 0;
  let data = {
    tecnica : {
      creo: 0,
      muto: 0,
      intellego: 0,
      rego: 0,
      perdo: 0
    },
    forma : {
      corpus: 0,
      herbam: 0,
      animal: 0,
      ignem: 0,
      terram: 0,
      auram: 0,
      imaginem: 0,
      mentem: 0,
      vim: 0
    },
    inteligencia : 0,
    teoriaMagica : 0
  };
  const appData = BaseDirectory.AppData;


  function next(){
    currentState += 1;
    updateViewportComponent();
  }


  function config(){
    currentState = 0;
    updateViewportComponent();
  }

  function updateViewportComponent(){
    viewportComponent = states[currentState];
  }


  fs.readTextFile("data.json", {dir: appData}).then((response) => {
    if (response !== "") {
      console.log(response);
      data = JSON.parse(response);
      console.log(data);
      next();
    }
  }).catch(() => {
    fs.writeTextFile({path:"data.json"}, {dir: appData});
  })

  updateViewportComponent();

</script>

<main class="container">
  <h1 id="title">Echiso Creador</h1>
  <hr>
  {#if currentState!==0}
    <button id="configButton" on:click={config}>Configurar</button>
  {/if}

  <div id="viewport">
    <svelte:component this={viewportComponent} on:next={next} bind:data={data}></svelte:component>
  </div>

</main>

<style>
  hr {
    width: 70%;
  }
  *{
    margin: auto;
  }
  .container{
    padding-top: 25px;
  }
  #title{
    text-align: center;
    padding-bottom: 25px;
  }
  #configButton{
    position: absolute;
    top: 0;
    right: 0;
    margin-top: 10px;
    margin-right: 20px;
  }

</style>