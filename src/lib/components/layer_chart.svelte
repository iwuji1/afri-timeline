<script>
  import Data from "$lib/Data/inde_flags.json";
  import Period from '$lib/components/periods.svelte';

  const year_themes = [
    {"theme":"1847 - 1950",
  "description":"Stiring the pot"},
    {"theme":"1951 - 1959",
  "description":"The Bridge"},
    {"theme":"1960",
  "description":"Liberation from the west"},
    {"theme":"1961 - 1972",
  "description":"We still going"},
    {"theme":"1973 - 1989",
  "description":"Another jump"},
    {"theme":"1990 - Present",
  "description":"The new commers & Future"}
  ]

  // window.onscroll = function() {myFunction()};
  //
  // var header = document.getElementById("intbar");
  // var sticky = header.offsetTop;
  //
  // function myFunction() {
  //   if (window.pageYOffset > sticky) {
  //     header.classList.add("sticky");
  //   } else {
  //     header.classList.remove("sticky");
  //   }
  // }
</script>

<style>

  * {
    box-sizing: border-box;
  }
  .div-container {
    display: flex;
    flex-direction: column;
    margin: auto;
    background: papayawhip;
    font-family:sans-serif;
  }

  .div-container h1 {
    color: #800080;
    font-size: 40px;
  }

  .div-container p {
    font-weight: 400;
    font-size: 30px;
  }


  .flag-spec {
    display: flex;
    background-color: #e08214;
    margin-top: 5%;
    width: 100vw;
    font-family:sans-serif;
  }

  .left-content {
    flex: 50%;
    margin:auto;
  }

  .right-content {
    display: grid;
    justify-content: start;
    grid-template-columns: auto auto auto;
    gap: 10px;
    padding: 10px;
  }

  .flag-spec h1{
    font-size: 40px;
    color: #800080;
  }

  .flag-spec p{
    color: #ffffff;
    font-weight: 400;
    font-size: 30px;
  }

  .flag {
    align-self: content;
  }

  img {
    width: 100%;
    height: auto;
  }

  .inbar {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    background: papayawhip;
  }

  .sticky {
    position: fixed;
    top: 0;
    width: 100%;
  }

  .int-link {
    font-weight: bold;
    font-size: 20px;
    text-transform: uppercase;
    text-decoration: none;
    color: #e08214;
    padding: 20px 0px;
    margin: 0px 20px;
    display: inline-block;
    position: relative;
    opacity: 0.75;
  }

</style>

<div class="div-container">
  <div>
    <h1>What are we looking at?</h1>
    <p>What we have been looking at in the project is the reimagining of a table with static dates of African Independence, to something a bit more dynamic
    that tells a story. After going through the previous visualizations, I think a story does come to light, by splitting the various years into specific
    buckets, we can see various themes in the journey to an Independent Africa. Here the years are packaged into year buckets with the corresponding countries
    represented by their flag. Can you guess which countries come under which bucket?
    </p>
    <div id="intbar" class="intbar">
      {#each year_themes as t}
          <a class="int-link" href="#{t.description}">{t.description}</a>
      {/each}
    </div>
  </div>


  {#each year_themes as t}
    <div id={t.description} class="flag-spec">
      <div class="left-content">
        <h1>{t.theme}</h1>
        <p>{t.description}</p>
      </div>
        <div class="right-content">
          {#each Data as d}
            {#if d.Theme == t.description}
                <img class="flag" src={d.Img_URL} alt="" />
                <text class="leg-text" text-anchor="middle">{d.Country}</text>

            {/if}
          {/each}
        </div>
      </div>
  {/each}
</div>
