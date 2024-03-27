<script>
  import * as d3 from "d3"
  import IrregularPath from "./lib/IrregularPath.svelte"
</script>

<main>
  <h1 id="titulo">Línea D</h1>
  <h3 id="subt">Porcentaje del Trayecto Realizado</h3>
  <!-- 1. Canal: altura. Tipo: col con divs -->
  <IrregularPath />
</main>

<style>
  h1, h3 {
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    text-align: center;
  }

  #titulo {
    font-weight: bold;
    font-size: 50px;
    background-color: #00640E;
    color: white;
  }

  #subt {
    color: #00640E;
    letter-spacing: 1px;
    font-size: 30px;
    font-weight: bold;
  }

</style>
