<script>
  // components imports
  import ProgramCard from "$lib/molecules/programcard.svelte";
  import ScheduleTimes from "../atoms/schedule-times.svelte";

  // General imports
  import { onMount } from "svelte";

  // data import
  export let data;
  // let { data } = $props();

  function getImageSource(show) {
    const programShow = show.mh_shows_id.show;

    // Pakt de eerste user op van de show
    const firstUser =
      programShow &&
      programShow.users &&
      programShow.users[0] &&
      programShow.users[0].mh_users_id &&
      programShow.users[0].mh_users_id.cover;

    // Pakt de thumbnail van de show

    const thumbnail =
      programShow && programShow.thumbnail && programShow.thumbnail.id;

    // Als de cover niet bestaat of er geen users zijn, gebruik dan de thumbnail van de show
    // Als er geen thumbnail of cover is gebruik een lege string
    return firstUser ? `/${firstUser}` : thumbnail ? `/${thumbnail}` : "";
  }

  // Helper function to get the show time
  function getShowTime(show) {
    const showId = show.mh_shows_id;
    // Haalt de tijden op, als er geen tijden zijn, gebruik dan 00:00
    const from = showId && showId.from ? showId.from : "00:00";
    const until = showId && showId.until ? showId.until : "00:00";

    // Verkleint de tijd van 04:00:00 naar 04:00
    const formattedFrom = from.slice(0, 5);
    const formattedUntil = until.slice(0, 5);

    return `${formattedFrom} - ${formattedUntil}`;
  }

  // groepeer de radio stations
  function groupByRadioStation(shows) {
    const radioStation = {};

    for (const show of shows) {
      const showId = show.mh_shows_id;

      const programShow = showId && showId.show;
      const station = programShow && programShow.radiostation;
      const stationName = station && station.name;
      const stationImage = station && station.logo && station.logo.id;

      if (!radioStation[stationName]) {
        radioStation[stationName] = [];
      }

      radioStation[stationName].push(show);
    }

    // Sort each station's shows by 'from' time
    for (const stationName in radioStation) {
      radioStation[stationName].sort((a, b) => {
        const fromA = a.mh_shows_id?.from || "00:00";
        const fromB = b.mh_shows_id?.from || "00:00";
        return fromA.localeCompare(fromB);
      });
    }

    return radioStation;
  }

  // Groepeer de shows per radio station (dit is de call)
  const groupedShows = groupByRadioStation(
    (data && data.data && data.data[0] && data.data[0].shows) || [],
  );

  const updateScheduleLine = () => {
    const date = new Date();
    const minutes = (100 / 60) * date.getMinutes(); // Convert minutes to time units
    const timeValue = date.getHours() * 100 + minutes; // Current time in "HHMM" format

    const totalColumns = Math.floor(2359 / 2.02); // Total number of grid columns
    const gridPosition = (timeValue / 2359) * totalColumns; // Position in the grid

    const line = document.querySelector(".schedule-line");
    if (line) {
      line.style.setProperty("--timepassed", `${gridPosition * 3}px`); // Adjust to match column width (3px)
      line.style.display = "block";
    }
  };

  onMount(() => {
    updateScheduleLine();
    setInterval(updateScheduleLine, 1000);
  });
</script>

<div class="display-screen"><p>Scroll to see schedule</p></div>

<div class="schedule">
  {#if Object.keys(groupedShows).length > 0}
    {#each Object.entries(groupedShows) as [stationName, stationShows]}
      <div class="schedule__radio-station-row">
        <div class="schedule__station-shows">
          {#each stationShows as show, i}
            <ProgramCard
              programName={show.mh_shows_id?.show?.name || "Unknown Program"}
              time={getShowTime(show)}
              imgSrc={getImageSource(show)}
              programLink={`/`}
            />
          {/each}
        </div>
      </div>
    {/each}
  {:else}
    <p>No programs available</p>
  {/if}
</div>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Merienda:wght@300..900&family=Nunito+Sans:ital,opsz,wght@0,6..12,200..1000;1,6..12,200..1000&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

  .display-screen {
    height: 50vh;
    background: white;
    display: none;
    animation:
      adjust-background linear forwards,
      adjust-intro-height linear forwards;
    animation-timeline: scroll(root block);
    /* animation-range: 50vh; */
    position: relative;
  }

  /* Set up Animation */
  @keyframes adjust-background {
    from {
      background: white;
    }

    to {
      background: transparent;
    }
  }

  .display-screen p {
    position: absolute;
    bottom: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: black;
    font-size: 3em;
    text-align: center;
    font-family: "Merienda", cursive;
    animation: adjust-color linear forwards;
    animation-timeline: scroll(root block);
    animation-range-end: 30vh;
  }

  @keyframes adjust-color {
    from {
      color: black;
    }

    to {
      color: white;
    }
  }

  @keyframes adjust-intro-height {
    from {
      height: 50vh;
    }

    to {
      height: 40vh;
    }
  }

  .schedule {
    height: 100vh;
    overflow: auto;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    gap: 1rem;
    padding: 1rem;
    position: relative;

    @media (min-width: 40em) {
      padding: 2rem;
    }
  }

  .schedule__radio-station-row {
    align-items: center;
    display: flex;
    overflow: hidden;
  }

  .schedule__radio-station-row:nth-of-type(2) {
    transform: translateY(calc(-100% + 100vh));
    flex-direction: column-reverse;
    animation: adjust-position linear forwards;
    animation-timeline: scroll(block);
    /* animation-range-end: 20vh; */
  }

  @keyframes adjust-position {
    from {
      transform: translateY(calc(-100% + 100vh));
    }

    to {
      transform: translateY(calc(100% - 100vh));
    }
  }

  .schedule__station-shows {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  img {
    height: 100px;
    margin-right: 1rem;
    padding: 20px;
    width: 100px;
  }
</style>
