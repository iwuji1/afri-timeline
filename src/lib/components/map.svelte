<script>

  import * as d3 from 'd3';
  import { scaleBand, scaleLinear } from "d3-scale";
  import { onMount } from 'svelte';
  import mapboxgl from "mapbox-gl";
  import 'mapbox-gl/dist/mapbox-gl.css';

  import Legend from '$lib/components/map_legend.svelte';
  import Tooltip from '$lib/components/map_tooltip.svelte';
  import dots from "$lib/Data/africa.json";

  let map;
  let mapx;
  let mapy;
  let hoverData;
  let width = 1000;
  let height = 800;
  const subgroups = ["United_States", "Britain", "Italy", "Britain_Egypt", "France", "Spain", "Belgium", "Portugal", "South_Africa", "Ethiopia"];

  $: cScale = d3.scaleOrdinal().domain(subgroups).range(["#2d004b","#800080","#8073ac","#b2abd2","#d8daeb","#f7f7f7","#fee0b6","#fdb863","#e08214","#b35806","#7f3b08"]);

  mapboxgl.accessToken = 'pk.eyJ1Ijoib2Jpd3VqaSIsImEiOiJja3B3ZHdvenkwMHV4MnFucHc2YW9tcHcyIn0.wI9Kn7vACQdq61dnjStghg';

  onMount(() => {
    map = new mapboxgl.Map({
        container: 'map', // container id
        style: 'mapbox://styles/mapbox/streets-v9',
        center: [15, -6],
        liglatbounds: ([-73.9876, 40.7661], [-73.9397, 40.8002]),
        zoom: 2.5,
        interactive: false,
    });

    // Projection method:
    // Project geojson coordinate to the map's current state
  })
</script>

<style>
  .map-container {
    position: relative;
    width: 100vw;
    height: auto;
    font-family: sans-serif;
  }

  #map {
    position: absolute;
    width: 100vw;
    height: 100vh;
    margin:0;
    padding: 0;
  }

  svg {
    position: absolute;
  }

</style>
<div class="map-container"
  bind:clientWidth={width}
  on:mouseleave={() => {
    hoverData = null;
    }}>
  <div id="map"></div>
    <svg width="100%" {height}>
    {#each dots as d}
      {#if map}
        <circle class="map-dots"
          cx={map.project(d.geometry.coordinates).x}
          cy={map.project(d.geometry.coordinates).y}
          r="5"
          fill={cScale(d.properties.colonizer)}
          stroke={hoverData && hoverData == d ?"#F7931E":"#800080" }
          stroke-width={hoverData && hoverData == d ?"2":"0" }
          on:mouseover={() => {
            hoverData = d
            mapx = map.project(d.geometry.coordinates).x
            mapy = map.project(d.geometry.coordinates).y
            }}
          on:focus={() => {
            hoverData = d
            mapx = map.project(d.geometry.coordinates).x
            mapy = map.project(d.geometry.coordinates).y
            }}
        />
      {/if}
    {/each}
    </svg>
  <Legend data={subgroups} {cScale}/>
  {#if hoverData}
    <Tooltip data={hoverData} {mapx} {mapy}/>
  {/if}
</div>
