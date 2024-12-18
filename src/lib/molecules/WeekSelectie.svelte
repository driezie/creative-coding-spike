<script>
  // maak een functie die het jaar en maand meeneemt
  const loadMonthDays = (year, month) => {
    // Maak een array met daarin de weekdagen
    const daysOfWeek = [
      "zondag",
      "maandag",
      "dinsdag",
      "woensdag",
      "donderdag",
      "vrijdag",
      "zaterdag",
    ];
    // Aantal dagen in de maand
    let daysInMonth = new Date(year, month + 1, 0).getDate();
    // Maak een lege array waarin de maanddagen komen
    let monthDays = [];
    // Loop door alle dagen van de maand
    for (let day = 1; day <= daysInMonth; day++) {
      // voor elke dag in de loop wordt een date gemaakt die het jaar, de dag en de maand bevat
      let date = new Date(year, month, day);
      // met date.getDay haal je de dagnaam op aan de hand van een nummer in de array
      let dayOfWeek = daysOfWeek[date.getDay()];
      // Voeg de naam van de dag in de monthDays array
      monthDays.push({ dayOfWeek, day });
    }
    // Geef de waarde van monthday array terug
    return monthDays;
  };
  // Haal de tijd en datum van vandaag op
  let dateAndTime = new Date();
  //  haal het huidige jaar op
  let year = dateAndTime.getFullYear();
  // Haal de huidige maand op
  let month = dateAndTime.getMonth();
  // Haal de dagen en de maand van het huidige jaar op en stop deze in de variabele daysMonth
  let daysInMonth = loadMonthDays(year, month);
  // Maak de variabele carousel aan
  let carousel;
  // haal de huidige dag op
  let currentDayNumber = dateAndTime.getDate();
  // Create an array that shows al the month names in the right order
  const monthNames = [
  "januari",
  "februari",
  "maart",
  "april",
  "mei",
  "juni",
  "juli",
  "augustus",
  "september",
  "oktober",
  "november",
  "december",
  ];
  // Get the name of the month, the month variable gives the current month in a digit, I use this value to get the right name of the month from the array
  let showCurrentMonth = monthNames[month];
  // Scroll funcies
  const scrollLeft = () => carousel?.scrollBy({ left: -200, behavior: "smooth" });
  const scrollRight = () => carousel?.scrollBy({ left: 200, behavior: "smooth" });
</script>

<!-- HTML -->
<section class="month-overview">
  <!-- Get the current month and year value from the variables and print it on the screen -->
<h2>{showCurrentMonth} {year}</h2>
<section class="day-carousel">
  <button
    class="navigation-buttons"
    on:click={scrollLeft}
  >
    <svg
      width="28"
      height="36"
      viewBox="0 0 7 12"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <title>Scroll naar links</title>
      <path
        d="M5.86317 11.5298C6.12271 11.2703 6.12285 10.8496 5.86349 10.5898L2.17915 6.90044C1.78908 6.50984 1.7893 5.87705 2.17963 5.48671L5.86287 1.80347C6.12252 1.54382 6.12252 1.12285 5.86287 0.863198V0.863198C5.60333 0.603655 5.18257 0.603534 4.92287 0.862928L0.294261 5.48623C-0.0966467 5.87669 -0.0968283 6.51016 0.293855 6.90085L4.92285 11.5298C5.18251 11.7895 5.60351 11.7895 5.86317 11.5298V11.5298Z"
        fill="white"
      />
    </svg>
  </button>
  <!-- Koppel het variabele carousel aan de ol -->
  <ol bind:this={carousel}>
    <!-- Ga de daysinmonth array af en geef de uitkomsten weer als dayofweek en day -->
    {#each daysInMonth as { dayOfWeek, day }}
    <li >
        <!-- als de dag gelijk is aan de nummer van de huidige dag krijgt de button de active class -->
        <button class:button-active={day === currentDayNumber} class:new-week={dayOfWeek === "zondag"}>
          <!-- Weergeef de dag in een string-->
          <span>{dayOfWeek}</span>
          <!-- Weergeef de dag als een nummer -->
          <span>{day}</span>
        </button>
      </li>
    {/each}
  </ol>
  <button
    class="navigation-buttons"
    on:click={scrollRight}
  >
    <svg
      width="28"
      height="36"
      viewBox="0 0 7 12"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <title>Scroll naar rechts</title>
      <path
        d="M1.13683 0.470161C0.877294 0.729698 0.87715 1.15045 1.13651 1.41016L4.82085 5.09956C5.21092 5.49016 5.2107 6.12295 4.82037 6.51329L1.13713 10.1965C0.877479 10.4562 0.877479 10.8772 1.13713 11.1368V11.1368C1.39667 11.3963 1.81743 11.3965 2.07713 11.1371L6.70574 6.51377C7.09665 6.12331 7.09683 5.48984 6.70615 5.09915L2.07715 0.470162C1.81749 0.210499 1.39649 0.210498 1.13683 0.470161V0.470161Z"
        fill="white"
      />
    </svg>
  </button>
</section>
</section>

<style>
  .month-overview{
    display: flex;
    flex-direction: column;
    align-items: center;
    @media screen and (min-width: 980px) {
      margin: 2em 18em 0 0;
    }
  }

  h2{
    font-size: 1.3em;
    margin: 0 auto;
    @media screen and (min-width: 500px) {
      font-size: 1.7em;
    }
  }
 .day-carousel {
    position: relative;
    display: flex;
    width: 60vw;
    overflow: hidden; /* Verberg inhoud die buiten het zicht valt */
    /* margin-left: calc(2rem + 105px); */
    @media screen and (min-width: 960px) {
      font-size: 1.5em;
    }
    @media screen and (min-width: 500px) {
    width: 50vw;
    
    }
  }

  ol {
    display: flex;
    overflow-x: scroll;
    scroll-behavior: smooth;
    scroll-snap-type: x mandatory;
    margin: 0;
    padding: 0;
    position: relative;
  }

  button.navigation-buttons {
    position: relative;
    z-index: 2; /* Zorg dat de knoppen boven de blur-elementen staan */
  }

  .day-carousel::before,
  .day-carousel::after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    width: 3em; /* Breedte van de blur aan beide kanten */
    pointer-events: none; /* Laat klikken door naar de knoppen */
    z-index: 1; /* Plaats de blur onder de knoppen */
  }

  .day-carousel::before {
    left: 1em; /* Plaats de blur naast de eerste knop */
    background: linear-gradient(
      to right,
      rgba(255, 255, 255, 1),
      rgba(255, 255, 255, 0)
    ); /* Linker blur */
  }

  .day-carousel::after {
    right: 1em; /* Plaats de blur naast de laatste knop */
    background: linear-gradient(
      to left,
      rgba(255, 255, 255, 1),
      rgba(255, 255, 255, 0)
    ); /* Rechter blur */
  }

  button {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border: none;
    outline: none;
    background-color: rgb(239, 239, 239);
    font-family: var(--font-family);
    padding: 1em;
    font-size: 0.9em;
    cursor: pointer;
    font-weight: bold;
    @media (prefers-reduced-motion: no-preference) {
      transition: 0.2s ease-in;
    }
  }
 
  .button-active {
    background-color: var(--secondary-color);
    color: var(--light);
  }

  .button-active span:first-of-type {
    color: var(--light);
  }

  li  button:hover,
  li button:focus
  {
    background-color: var(--primary-color);
    color: var(--light);
    border-radius: 15px;
    @media (prefers-reduced-motion: no-preference) {
      scale: 0.9;
    }
  }

  button:hover span:first-of-type,
  button:focus span:first-of-type {
    color: var(--light);
  }

  button span:first-of-type {
color: #5D5D5D;
font-size: 0.8em;
  }

  button span:nth-of-type(2){
    font-size: 1.5em;
  }

  .navigation-buttons {
    background-color: var(--primary-color);
    padding: 0.5em;
  }

  .navigation-buttons:hover,
  .navigation-buttons:focus {
    background-color: var(--hover-secondary);
    @media (prefers-reduced-motion: no-preference) {
      scale: 0.9;
    }
  }
  
  .navigation-buttons:first-of-type {
    border-top-left-radius: 7px;
    border-bottom-left-radius: 7px;
  }

  .navigation-buttons:last-of-type {
    border-top-right-radius: 7px;
    border-bottom-right-radius: 7px;
  }

  .new-week {
    border-right: solid 8px var(--secondary-color);

    @media screen and (min-width: 960px) {
      border-right: solid 10px var(--secondary-color);

    }
  }
</style>
