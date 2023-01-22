<svelte:head>
</svelte:head>

<script>
  import Bar from '$lib/components/bar_chart.svelte'
  import Stacked from '$lib/components/stacked_chart.svelte'
  import Map from '$lib/components/map.svelte'
  import Period from '$lib/components/periods.svelte'
  import Layer from '$lib/components/layer_chart.svelte'

  import { onMount } from 'svelte';
  import gsap from "gsap";
  import {ScrollTrigger }from "gsap/dist/ScrollTrigger";

  gsap.registerPlugin(ScrollTrigger);


  onMount(() => {

    ScrollTrigger.create({
      start: 'top -80',
      end: 99999,
      toggleClass: {className: 'navbar--scrolled', targets: '.navbar'}
    });

    gsap.from("rect.bars", {
      scrollTrigger:{
        trigger:".viz",
        start: "top 90%",
        toggleActions: "restart pause resume pause"
      },
      width:0,
      duration: 2,
      stagger: {
        amount: 1.5,
      }
    });

    gsap.from("rect.group-rect", {
      scrollTrigger: {
        trigger:".stack-viz",
        start: "top 90%",
        toggleActions: "restart pause resume pause"
      },
      height:0,
      duration: 1.5,
      stagger: {
        amount: 1.5,
      }
    });

    gsap.from(".viz-text", {
      scrollTrigger: {
        trigger:".viz-text",
        start: "top 90%",
        toggleActions: "restart pause resume pause"
      },
      duration: 1.5,
      opacity:0,
      x:"50%"
    });

    gsap.from(".stack-text", {
      scrollTrigger: {
        trigger:".stack-text",
        start: "top 90%",
        toggleActions: "restart pause resume pause"
      },
      duration: 2,
      opacity:0,
      y:"50%"
    });

    const map_timeline = gsap.timeline({
      scrollTrigger: {
        trigger: '.map-container',
        start: 'top top',
        end: '+=80%',
        scrub: true,
        pin: true,
        anticipatePin: 1,
        toggleActions: "play none reverse none"
      }
    });

    map_timeline.to(".map-text", { duration: 0.33, opacity: 1, y:"50%" })
    .to(".map-text", { duration: 0.33, opacity: 0, y:"0%" }, 0.66);

    // gsap.to(".panel:not(:last-child)", {
    //   yPercent: -100,
    //   ease: "none",
    //   stagger: 0.5,
    //   scrollTrigger: {
    //     trigger: "#container",
    //     start: "top top",
    //     end: "+=300%",
    //     scrub: true,
    //     pin: true
    //   }
    // });

    // gsap.set(".panel", {zIndex: (i, target, targets) => targets.length - i});

  })

</script>

<style>

  .title {
    margin: auto;
    font-family:sans-serif;
  }

  .container {
    display: flex;
    padding-left: 5%;
    padding-right: 5%;
    margin: auto;
    height: 100vh;
  }

  .v-container {
    display: flex;
    padding-left: 5%;
    padding-right: 5%;
    flex-direction: column;
    /* height: 100vh; */
  }

  .mv-container {
    display: flex;
    flex-direction: column;
    padding: 0%;
    margin: 0%;
    height: 100vh;
  }

  .layer-container {
    display: flex;
    margin: auto auto;
  }

  .p-container {
    flex: 100%;
    display: flex;
    padding-left: 5%;
    padding-right: 5%;
    margin: auto;
    height: 100vh;
    margin: auto;
  }

  .viz {
    flex: 30%;
    margin:auto;
  }

  .viz-text {
    flex: 70%;
    margin:auto;
    padding-right: 10%;
    font-size: 18pt;
    font-family: sans-serif;

  }

  .map-text {
    position: absolute;
    justify-content: center;
    background-color: white;
    font-size: 18pt;
    font-family: sans-serif;
    margin: auto;
    margin-left: 35%;
    width: 30vw;
    text-align: center;
    transform:translateY(100%);
    opacity: 0;
  }



  .m-text p {
    font-family: sans-serif;
    font-weight: 100;
  }

  .stack-viz{
    flex:100%;
    margin: auto;
  }

  .stack-text {
    flex: 70%;
    margin:auto;
    padding-right: 10%;
    font-size: 18pt;
    font-family: sans-serif;
  }

  .map-viz {

  }

</style>

<div id="container">
  <section id="Title" class="panel container">
    <div class="title">
      <h1>A different look at African independence.</h1>
      <p>I was looking at the dates of African independence for various countries for a video
      I was making. And came across this website with the different dates <a href="https://www.thoughtco.com/chronological-list-of-african-independence-4070467">Awesome resource!</a>.
      </p>
      <p>But it did make me think, there is actually a lot of data in this table, how can I get different insights from this table
      and perhaps visualize African independence in a different way.
      </p>

      <h1>I hope you enjoy scrolling!</h1>

    </div>
  </section>

  <section id="who" class="panel container">
    <div class="viz">
    <Bar />
    </div>
    <div class="viz-text">
      <h1>Who were the Colonizers?</h1>
      <p>It doesn't take a history buff to not that much of the colonization of the African continent was attributed to the Europeans who went out into the
      world is such of resources and cheap labour. But who were the real forces driving the mission??</p>

      <p>It turns out whilst Britain was definitely a leader in the pack controlling 21 nations,
      France was equally an equally dominant force taking 20 nations. Spain and Portugal also played a
      key role among others. As we look into the timeline below we can learn more about what this looked like.</p>
    </div>
  </section>

  <section id="when" class="panel v-container">
    <div class="stack-text">
      <h1>When did African nations gain independence?</h1>
      <p>In this viz we arrange the data to understand what years nations became independent and who they gained interdependence from.
      You can definitely see leading up to 1960 the momentum that was happening as year after year of different nations getting theirs
      led to this major peak in 1960 where the majority of African nations got their independence. With Britain and France specifically
      losing their hold on many nations, it didn't take long for other colonizers to suffer the same fate.</p>
    </div>
    <div class="stack-viz">
    <Stacked />
    </div>
  </section>

  <section id="where" class="panel mv-container">
    <div class="map-viz">
      <Map />
    </div>
    <div class="map-text">
      <div class="m-text">
        <h1>Which countries got taken over?</h1>
      </div>
      <div class="m-text">
        <p>According to the webster dictionary the definition of colonization is:</p>
        <blockquote>The subjugation of a people or area especially as an extension of state power</blockquote>
      </div>
      <div class="m-text">
        <p>In the 1800’s European nations had a desire to get a lead to widespread imperialism in Africa.
          Why? Well besides the belief that, at the time, they were better than everyone else there were 2 main reasons:
           Expansion of territory with the limited land potential in europe, the opportunity to acquire land and natural resources was very appetizing
         and of course...Money. And so the scramble for Africa began, it got so intense at times that there was fear that war between Eurpean nations.</p>
      </div>
      <div class="m-text">
        <p>In the infamous words of Edwin starr "war...what is it good for, absolutely nothing".
        So to avoid the potential for war The Berlin Conference came to be in Feb 26, 1885. In this meeting, the Europeans divided up the land of africa,
      determining who owned which territory (the people living there currently obviously did not count), creating the map of Africa we see to day. Excluding
    Ethipoia and Liberia every African nation that we now know to day was put under the rule of a nation.</p>
      </div>
    </div>
  </section>

  <section id="how" class="p-container">
    <Period />
  </section>

  <section id="what" class="layer-container">
    <Layer />
  </section>

  <section id="end" class="panel container">
    <div class="title">
      <h1>And that's the end!</h1>

      <h2>Hope you enjoyed the story, here is the link the <a href="https://www.thoughtco.com/chronological-list-of-african-independence-4070467">Original article</a></h2>

    </div>
  </section>
</div>
