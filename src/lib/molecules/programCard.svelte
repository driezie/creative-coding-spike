<script>
  // General imports
  import { onMount } from "svelte";
  import Clock from "$lib/atoms/icon.svelte";

  // data import
  export let status = "";
  export let imgSrc = "";
  export let programName = "Unnamed Program";
  export let time = "00:00 - 00:00";
  export let programLink = "/";

  // Time splitting
  let parts = time.split(" - ");
  let tempstart = parseInt(parts[0].replace(":", ""));
  let tempend = parseInt(parts[1].replace(":", ""));

  // Calc zodat de grid niet te groot wordt
  const start = tempstart / 2.02;
  const end = tempend / 2.02;

  const updateStatus = () => {
    const date = new Date();
    const currentTime = date.getHours() * 100 + date.getMinutes();
    status = tempstart <= currentTime && currentTime <= tempend ? "active" : "";
  };

  onMount(() => {
    updateStatus();
    setInterval(updateStatus, 60000);
  });
</script>

<a class="card {status}" href={programLink}>
  <!-- <picture class="image">
    <source
      srcset={imgSrc
        ? `https://fdnd-agency.directus.app/assets/${imgSrc}?format=webp`
        : "/path/to/default/image.jpg"}
      alt={programName}
    />
    <source
      srcset={imgSrc
        ? `https://fdnd-agency.directus.app/assets/${imgSrc}?format=jpg`
        : "/path/to/default/image.jpg"}
      alt={programName}
    />
    <img
      loading="lazy"
      src={imgSrc
        ? `https://fdnd-agency.directus.app/assets/${imgSrc}?format=jpeg`
        : "/path/to/default/image.jpg"}
      alt={programName}
    />
  </picture> -->

  <!-- <article class="content">
    <div class="title-wrapper">
      <h2>{programName}</h2>
    </div>

    <div class="events">
      <div class="time-stamp">
        <Clock data={tempstart} />
        <span>{time}</span>
      </div>


    </div>
  </article> -->
</a>

<style>
  :root {
    --calc: calc(2rem - 1rem);
  }

  .card {
    background: white;
    display: flex;
    height: auto;
    width: auto;
    height: 30vh;
    width: 10rem;
  }

  .card {
    /* animation: show-card linear forwards;
    animation-timeline: scroll(root block); */
  }

  /* Set up Animation */
  @keyframes show-card {
    /* Start position: shift entire column up, but not so that it goes out of view */
    0% {
      opacity: 0;
    }

    /* End position: shift entire column down, but not so that it goes out of view */
    50% {
      opacity: 1;
    }

    100% {
      opacity: 0;
    }
  }

  .card article {
    display: none;
  }

  @media (prefers-reduced-motion) {
  }

  img,
  picture {
    object-fit: cover;
    height: 100%;
    width: auto;
  }
</style>
