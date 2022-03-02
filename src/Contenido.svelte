<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Animales  from "./Animales.svelte";
  import Cuidadores   from "./Cuidadores.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/animales" component={Animales} />
  <Route path="/cuidadores" component={Cuidadores} />
</main>
