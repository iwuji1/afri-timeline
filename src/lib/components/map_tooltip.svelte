<script>
  export let data;
  export let mapx;
  export let mapy;


  import { onMount } from 'svelte';
  import mapboxgl from "mapbox-gl";

  let map2;

  // onMount(() => {
  //   map2 = new mapboxgl.Map({
  //       container: 'map', // container id
  //       style: 'mapbox://styles/mapbox/streets-v9',
  //       center: [15, -6],
  //       liglatbounds: ([-73.9876, 40.7661], [-73.9397, 40.8002]),
  //       zoom: 3,
  //       interactive: false,
  //   });
  //
  // })

</script>

<style>

  .tooltip{
    padding: 2px;
    background: #ffffff;
    pointer-events: none;
    transition: top 300ms ease, left 300ms ease;
    opacity: 0.75;
  }

  h3 {
    font-weight: 700;
    font-family:sans-serif;
    margin-bottom: 0.1rem;
  }

</style>

<div class="tooltip"
  style="
  position: absolute;
  top: {mapy}px;
  left:{mapx}px">
  <h3>Country: {data.properties.country}</h3>
  <p>Colonizer: {data.properties.colonizer}</p>

  </div>
