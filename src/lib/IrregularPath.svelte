<script>
  import {onMount} from "svelte"
  import * as d3 from "d3"

  let numbers = [10, 25, 33, 62, 75, 100]
  let pathLength
  let largo
  let circles = [ //para pintar los circulos a medida que aumenta el progreso sobre el recorrido
    { id: 'p1', cx: 42, cy: 70, threshold: 10 },
    { id: 'p2', cx: 62, cy: 98, threshold: 16 },
    { id: 'p3', cx: 94, cy: 130, threshold: 24 },
    { id: 'p4', cx: 134, cy: 166, threshold: 33 },
    { id: 'p5', cx: 174, cy: 186, threshold: 42 },
    { id: 'p6', cx: 194, cy: 210, threshold: 47 },
    { id: 'p7', cx: 218, cy: 234, threshold: 53 },
    { id: 'p8', cx: 238, cy: 258, threshold: 59 },
    { id: 'p9', cx: 254, cy: 282, threshold: 64 },
    { id: 'p10', cx: 274, cy: 306, threshold: 69 },
    { id: 'p11', cx: 294, cy: 338, threshold: 80 },
    { id: 'p12', cx: 354, cy: 354, threshold: 89 },
    { id: 'p13', cx: 370, cy: 374, threshold: 93 },
    { id: 'p14', cx: 398, cy: 398, threshold: 100 }
  ];


  onMount(() => {
    // @ts-ignore
    // longitud total del path
    pathLength = document.querySelector("#polyline").getTotalLength()
    // longitud total del path
    let maxGap = pathLength - (pathLength * d3.min(numbers) / d3.max(numbers))
    let minGap = 0

    largo = function (n) {
      let scale = d3
        .scaleLinear()
        .domain(d3.extent(numbers)) // extent returns [min, max]
        .range([maxGap, minGap])
      return scale(n)
    }
  })
</script>

<div class="linea">
{#each numbers as n}
    <div class="grafico">
      <svg width="410" height="440">
        <!-- Linea D -->
        <polyline id="polyline"
          points="10.8,28 42,70 62,98 94,130 134,166 174,186 194,210 218,234 238,258 254,282 274,306 294,338 354,354 370,374 398,398"
          fill="transparent"
          stroke="#ccc"
          stroke-width="5"
        />
        <g id="puntos">
          <circle cx="10.8" cy="28" r="5" fill="white" stroke="black" />
          <text x="35.45" y="8" text-anchor="middle" alignment-baseline="middle">Congreso</text>
          <circle cx="42" cy="70" r="5" fill="white" stroke="black"/>
          <circle cx="62" cy="98" r="5" fill="white" stroke="black"/>
          <circle cx="94" cy="130" r="5" fill="white" stroke="black" />
          <circle cx="134" cy="166" r="5" fill="white" stroke="black" />
          <circle cx="174" cy="186" r="5" fill="white" stroke="black" />
          <circle cx="194" cy="210" r="5" fill="white" stroke="black" />
          <circle cx="218" cy="234" r="5" fill="white" stroke="black" />
          <circle cx="238" cy="258" r="5" fill="white" stroke="black" />
          <circle cx="254" cy="282" r="5" fill="white" stroke="black" />
          <circle cx="274" cy="306" r="5" fill="white" stroke="black" />
          <circle cx="294" cy="338" r="5" fill="white" stroke="black" />
          <circle cx="354" cy="354" r="5" fill="white" stroke="black" />
          <circle cx="370" cy="374" r="5" fill="white" stroke="black" />
          <circle cx="398" cy="398" r="5" fill="white" stroke="black" />
          <text x="378" y="420" text-anchor="middle" alignment-baseline="middle">Catedral</text>
        </g>


        <!-- Progreso -->
        {#if pathLength}
        <polyline id="polyline" 
            points="10.8,28 42,70 62,98 94,130 134,166 174,186 194,210 218,234 238,258 254,282 274,306 294,338 354,354 370,374 398,398"
            fill="none"
            stroke="green"
            stroke-width="5"
            stroke-dasharray={pathLength}
            stroke-dashoffset={largo(n)}
        />
        <g id="primera estacion">
          <circle  cx="10.8" cy="28" r="5" fill="green" stroke="green"/>
        </g>
        {/if}

        {#each circles as circle}
          {#if n >= circle.threshold}
            <circle id={circle.id} cx={circle.cx} cy={circle.cy} r="5" fill="green" stroke="green"/>
          {/if}
        {/each}
      
      </svg>
      
      <p class="porcentaje">{n}% del viaje realizado</p>

    </div>
    {/each}
  </div>

<style>
  .linea{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: space-between;
    
  }

  .grafico {
    margin-top: 20px;
    margin-bottom: 50px;
  }

  .porcentaje {
    text-align: center;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    font-size: 20px;
    color: #00640E
  }
</style>
