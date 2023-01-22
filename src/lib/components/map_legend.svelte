<script>
  export let cScale;
  export let data;

</script>

<style>

  .legend{
    /* position: absolute; */
    width: 15%;
    height: auto;
    border: 2px solid white;
    border-radius: 5px;
    margin-top: 5%;
    background: #ffffff;
    opacity: 80%;
  }

  .chart-title {
    text-align: center;
  }


</style>

<div class="legend">
  <h1 class="chart-title">Colonizers</h1>
  <svg width="300" height="280">
    {#each data as d,i}
      <text class="leg-txt" x="120" dy=".3em" y={20 + i*25}>{d}</text>
      <circle
        cx="100"
        cy={20 + i*25}
        r="7"
        fill={cScale(d)}/>
    {/each}
  </svg>
</div>
