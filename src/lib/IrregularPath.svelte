<script>
  import {onMount} from "svelte"
  import * as d3 from "d3"

  let numbers = [38, 100]
  let pathLength
  let largo


  onMount(() => {
    // @ts-ignore
    // longitud total del path
    pathLength = document.querySelector("#polyline").getTotalLength()
    // longitud total del path
    let maxGap = pathLength - (pathLength * d3.min(numbers) / d3.max(numbers))
    let minGap = 0

    // console.log("total path", pathLength)
    // console.log("maximo gap", maxGap)
    // console.log("minimo gap", maxGap)

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
    <div>
      <svg width="600" height="600">
        <!-- Linea D -->
        <polyline id="polyline"
          points="52.25,60 90,125 115,160 155,200 205,245 255,270 280,300 310,330 335,360 355,390 
          380,420 385,460 480,480 500,505 535,535"
          fill="transparent"
          stroke="#ccc"
          stroke-width="5"
        />
        <g id="puntos">
          <circle cx="52.25" cy="60" r="5" fill="white" stroke="black" />
          <text x="52.25" y="40" text-anchor="middle" alignment-baseline="middle">Congreso</text>
          <circle id="p1" cx="90" cy="125" r="5" fill="white" stroke="black"/>
          <circle id="p2" cx="115" cy="160" r="5" fill="white" stroke="black"/>
          <circle id="p3" cx="155" cy="200" r="5" fill="white" stroke="black" />
          <circle id="p4" cx="205" cy="245" r="5" fill="white" stroke="black" />
          <circle id="p5" cx="255" cy="270" r="5" fill="white" stroke="black" />
          <circle id="p6" cx="280" cy="300" r="5" fill="white" stroke="black" />
          <circle id="p7" cx="310" cy="330" r="5" fill="white" stroke="black" />
          <circle id="p8" cx="335" cy="360" r="5" fill="white" stroke="black" />
          <circle id="p9" cx="355" cy="390" r="5" fill="white" stroke="black" />
          <circle id="p10" cx="380" cy="420" r="5" fill="white" stroke="black" />
          <circle id="p11" cx="385" cy="460" r="5" fill="white" stroke="black" />
          <circle id="p12" cx="480" cy="480" r="5" fill="white" stroke="black" />
          <circle id="p13" cx="500" cy="505" r="5" fill="white" stroke="black" />
          <circle id="p14" cx="535" cy="535" r="5" fill="white" stroke="black" />
          <text x="535" y="555" text-anchor="middle" alignment-baseline="middle">Catedral</text>
        </g>


        <!-- Progreso -->
        {#if pathLength}
          <polyline id="polyline" 
              points="52.25,60 90,125 115,160 155,200 205,245 255,270 280,300 310,330 335,360 355,390 
              380,420 385,460 480,480 500,505 535,535"
              fill="none"
              stroke="green"
              stroke-width="5"
              stroke-dasharray={pathLength}
              stroke-dashoffset={largo(n)}
          />
          <g id="puntos">
            <circle  cx="52.25" cy="60" r="5" fill="green" stroke="black"/>
          </g>
        {/if}
        
        <!--{#each estaciones as e}
          {#if n >= e/14 * 100}
              <circle id={strEstaciones[e-1]} cx="90" cy="125" r="5" fill="green" stroke="black"/>
          {/if}
        {/each}-->
        
        
        {#if n >= 10}
          <circle id="p1" cx="90" cy="125" r="5" fill="green" stroke="black"/>
        {/if}

        {#if n >= 16}
          <circle id="p2" cx="115" cy="160" r="5" fill="green" stroke="black"/>
        {/if}

        {#if n >= 24}
          <circle id="p3" cx="155" cy="200" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 34}
          <circle id="p4" cx="205" cy="245" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 42}
          <circle id="p5" cx="255" cy="270" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 47}
          <circle id="p6" cx="280" cy="300" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 53}
          <circle id="p7" cx="310" cy="330" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 59}
          <circle id="p8" cx="335" cy="360" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 64}
          <circle id="p9" cx="355" cy="390" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 69}
          <circle id="p10" cx="380" cy="420" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 75}
        <circle id="p11" cx="385" cy="460" r="5" fill="green" stroke="black" />
        {/if}

        {#if n >= 89}
          <circle id="p12" cx="480" cy="480" r="5" fill="green" stroke="black" />
        {/if}
        
        {#if n >= 93}
          <circle id="p13" cx="500" cy="505" r="5" fill="green" stroke="black" />
        {/if}
        
        {#if n == 100}
          <circle id="p14" cx="535" cy="535" r="5" fill="green" stroke="black" />
        {/if}
        
      </svg>
      <p class="number">{n}% del viaje realizado</p>
    </div>
    {/each}
  </div>

<style>
  .linea{
    display: flex;
    /*flex-direction: column;*/
    flex-wrap: wrap;
    justify-content: center;
    align-items: space-between;
  }
  .number {
    text-align: center;
  }
</style>
