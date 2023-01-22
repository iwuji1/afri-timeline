<script>
  export let cScale;
  export let data;
  export let height;
  export let hoverData;

</script>

<style>

  .legend{
    background: #ffffff;
    width: 100%;
    height: auto;
  }

  .leg-text {

  }

</style>

<div class="legend">
  <svg width="250" height={height}>
    {#each data as d,i}
      <text class="leg-txt" x="120" dy=".3em" y={100 + i*25}>{d.key}</text>
      <circle
        cx="100"
        cy={100 + i*25}
        r="7"
        opacity={hoverData ? hoverData == d ? "1":".3" : "1"}
        fill={cScale(d.key)}/>
    {/each}
  </svg>
</div>
