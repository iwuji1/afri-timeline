<script>
  import * as d3 from 'd3';
  import { scaleBand, scaleLinear } from "d3-scale";
  import { max } from "d3-array";

  import Data2 from "$lib/Data/dates_independence2.js";
  import Legend from '$lib/components/legend_stack.svelte';

  let hoverData;

  let width = 1000;
  let height = 500;
  const subgroups = ["United_States", "Britain", "Italy", "Britain_Egypt", "France", "Spain", "Belgium", "Portugal", "South_Africa", "Ethiopia"]

  const margin = { top: 20, right: 10, left: 80, bottom: 20 };
  const innerHeight = height - margin.top - margin.bottom;
  const innerWidth = width - margin.left - margin.right;
  const stackedData = d3.stack().keys(subgroups)
  const stackedSeries = stackedData(Data2)

  $: xDomain = Data2.map(function(d) {return d.year})

  $: xScale = scaleBand().domain(xDomain).range([0, innerWidth]).padding(0.1);
  $: yScale = scaleLinear().domain([0,15]).range([innerHeight, 0]);
  $: cScale = d3.scaleOrdinal().domain(subgroups).range(["#2d004b","#800080","#8073ac","#b2abd2","#d8daeb","#f7f7f7","#fee0b6","#fdb863","#e08214","#b35806","#7f3b08"])

</script>
<style>
 .chart-container {
   display: flex;
   width: 100%;
   height: auto;
   font-family: sans-serif;
 }

 @media screen and (max-width: 1200px) {
   .chart-container {
     flex-direction: column;
   }

   svg {
     width: 50%;
     height: auto;
   }
 }

 .chart-txt {
   font-weight: 100;
 }

 h1 {
   font-size: 30px;
   font-weight: 600;
   margin-bottom: 0.5rem;
   font-family: sans-serif;
 }

</style>
<h1> What years were the peak of independence ?</h1>
<div class="chart-container">
  <div class="chart"
    bind:clientWidth={width}
    on:mouseleave={() => {
      hoverData = null;
      }}>
    <svg {width} {height}>
      <g transform={`translate(${margin.left},${margin.top})`}>
        {#each yScale.ticks() as tickValue}
          <g transform={`translate(0,${yScale(tickValue)})`}>
            <line x2={innerWidth} stroke="#cecece" />
            <text text-anchor="middle" dy=".7em" y={innerWidth}>
              {tickValue}
            </text>
          </g>
          {/each}
      {#each stackedSeries as d}
        {#each d as ind,i}
          <text class="chart-txt" text-anchor="middle" x={xScale(ind.data.year) + xScale.bandwidth() / 2} dy=".3em" y={innerHeight+10}>{ind.data.year}</text>
          <rect
            class='group-rect'
            y={yScale(ind[1])}
            x={xScale(ind.data.year)}
            width={xScale.bandwidth()}
            height={yScale(ind[0]) - yScale(ind[1])}
            opacity={hoverData ? hoverData == d ? "1":".3" : "1"}
            fill={cScale(d.key)}
            on:mouseover={() => {
              hoverData = d
              }}
            on:focus={() => {
              hoverData = d
              }}
              tabIndex="0"
            />
        {/each}
      {/each}
      </g>
    </svg>
  </div>
  <Legend data={stackedSeries} {hoverData} {cScale} {height}/>
</div>
