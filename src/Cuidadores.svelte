<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Cuidador                 from "./Cuidador.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let cuidador = {};

  onMount(async () => {
    const response = await fetch(URL.cuidadores);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>CUIDADORES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Cuidador bind:cuidador>
    <div style="text-align: right">
      <Boton documento={cuidador} tipo="insertar" coleccion="cuidadores" />
    </div>
  </Cuidador>
</div>

<div class="container">
  {#each datos as cuidador}
    <Cuidador {cuidador}>
      <div style="text-align: right">
        <Boton documento={cuidador} tipo="modificar" coleccion="cuidadores" />
        <Boton documento={cuidador} tipo="eliminar" coleccion="cuidadores" />
      </div>
    </Cuidador>
  {/each}
</div>