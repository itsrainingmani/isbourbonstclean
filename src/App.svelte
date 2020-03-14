<script>
  import { onMount } from "svelte";
  import moment from "moment-timezone";
  import Footer from "./Footer.svelte";
  let answer = "";

  let current = moment.tz("America/Chicago");
  $: currentTime = current.format("LT");

  onMount(() => {
    const interval = setInterval(() => {
      current = moment.tz("America/Chicago");
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });

  $: if (current.hour() >= 23 || current.hour() < 6) {
    if (current.hour() >= 0 && current.hour() < 3) {
      answer = "Fuck no";
    } else if (current.hour() >= 3 && current.hour() < 6) {
      answer = "🤢🤢🤢";
    }
  } else if (current.hour() >= 6 && current.hour() < 12) {
    answer = "So clean you could eat off the ground";
  } else if (current.hour() >= 12 && current.hour() < 18) {
    answer = "So .. Heck yeah!";
  } else if (current.hour() >= 18 && current.hour() < 23) {
    answer = "¯\\_(ツ)_/¯. I guess...";
  }
</script>

<style>
  main {
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
      url("../images/bourbon-street-day.jpg");
    height: 100%;

    /* Position and center the image to scale nicely on all screens */
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

    /* font stuff */
    font-family: "Overpass", sans-serif;
    text-align: center;
    /* max-width: 240px; */
    margin: 0 auto;
  }

  /* Place text in the middle of the image */
  .hero-text {
    width: 100%;
    text-align: center;
    position: absolute;
    top: 20%;
    left: 50%;
    transform: translate(-50%, -20%);
    color: white;
  }

  h1 {
    /* color: #000; */
    font-size: 4em;
    font-weight: 700;
    font-style: italic;
  }

  p {
    font-size: 2em;
    font-weight: 400;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  @media (max-width: 640px) {
    h1 {
      font-size: 2.75em;
    }

    p {
      font-size: 1.5em;
    }
  }
</style>

<main>
  <div class="hero-text">
    <h1>Is Bourbon Street Clean Now?</h1>
    <p>It's {currentTime} in N'awlins</p>
    <p>{answer}</p>
  </div>
</main>
<Footer />
