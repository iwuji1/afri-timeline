<script>

  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import { scaleBand, scaleLinear } from "d3-scale";
  import { max } from "d3-array";

  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  import Data from "$lib/Data/Colonizer.js";
  import Tooltip from '$lib/components/tooltip.svelte'

  let hoverData;

  let width = 800;
  let height = 600;

  const margin = { top: 20, right: 20, left: 120, bottom: 20 };
  const innerHeight = height - margin.top - margin.bottom;
  const innerWidth = width - margin.left - margin.right;

  $: xDomain = Data.map(function(d) {return d.Number_of_colonies});
  $: yDomain = Data.map(function(d) {return d.Colonizer});

  $: yScale = scaleBand().domain(yDomain).range([0, innerHeight]).padding(0.1);
  $: xScale = scaleLinear().domain([0,max(Data, function(d) {return d.Number_of_colonies})]).range([0, innerWidth]);


</script>

<style>
  rect {
    transition: opacity 300ms ease, fill 300ms ease;
    cursor: pointer;
  }

  rect:focus {
    outline: none;
  }

  h1 {
    font-size: 30px;
    font-weight: 600;
    margin-bottom: 0.5rem;
    font-family: sans-serif;
  }

  svg {
    font-family: sans-serif;
  }

  @media screen and (max-width: 1000px) {
    svg {
      width: 100%;
      height: auto;
    }


  }


</style>

<h1> Who had the most colonies ?</h1>

<div class="chart-container"
  bind:clientWidth={width}
  on:mouseleave={() => {
    hoverData = null;
    }}>
  <svg {width} {height}>
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each xScale.ticks() as tickValue}
        <g transform={`translate(${xScale(tickValue)},0)`}>
          <line y2={innerHeight} stroke="#cecece" />
          <text text-anchor="middle" dy=".7em" y={innerHeight + 3}>
            {tickValue}
          </text>
        </g>
      {/each}
      {#each Data.sort((a,b) => b.Number_of_colonies - a.Number_of_colonies) as d,i}
          <text text-anchor="end" x="-3" dy=".3em" y={yScale(d.Colonizer) + yScale.bandwidth() / 2}>
            {d.Colonizer}
          </text>
          <rect
            class="bars"
            x="0"
            y={yScale(d.Colonizer)}
            width={xScale(d.Number_of_colonies)}
            height={yScale.bandwidth()}
            opacity={hoverData ? hoverData == d ? "1":".3" : "1"}
            fill={hoverData && hoverData == d ?"#F7931E":"#800080" }
            on:mouseover={() => {
              hoverData = d
              }}
            on:focus={() => {
              hoverData = d
              }}
              tabIndex="0"
            />
        {/each}
    </g>
  </svg>
  {#if hoverData}
    <Tooltip data={hoverData} {xScale} {yScale}/>
  {/if}
</div>
