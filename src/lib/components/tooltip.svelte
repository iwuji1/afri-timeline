<script>
  export let data;
  export let xScale;
  export let yScale;
</script>

<style>

  .tooltip{
    padding: 2px;
    background: #ffffff;
    pointer-events: none;
    transition: top 300ms ease, left 300ms ease;
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
  top: {yScale(data.Colonizer)}px;
  left:{xScale(data.Number_of_colonies)}px">
  <h3>{data.Colonizer}</h3>
  <p>{data.Number_of_colonies} County(ies)</p>
</div>
