<script>
  import * as htmlToImage from "html-to-image";
  console.log(htmlToImage);

  import { onMount } from "svelte";
  import {
    savedCardNumber,
    topgradient,
    bottomgradient,
    lightbulbscolor,
  } from "$lib/stores/cardStore";
  import Fallingsnow from "$lib/atoms/christmas/fallingsnow.svelte";
  import Lightbulb from "$lib/atoms/christmas/lightbulb.svelte";
  import NumberButton from "$lib/atoms/numberButton.svelte";

  export let programLink = "";
  export let programName = "Unnamed Program";
  export let showLogo = "";
  export let thumbnailImgSrc = "";
  let PrimaryColors = ["#1b2d53", "#37508d", "#81a4dc"];
  // "#216789", "#c0cad6"
  let SecondaryColors = [
    "#2EBF61",
    "#FF272A",
    "#FFA500",
    "#FFD700",
    "#FFC0CB",
    "#FAFAFA",
  ];
  //
  let TertiaryColors = ["#E3DAD1", "#C0CAD6", "#F1EEE7", "#DEE5EB"];
  // "#FEFEFD"
  let Colors = [];

  function setpropertyofcolor(colorValue, color) {
    const card = document.getElementById(`popover-${programLink}-card`);
    const container = card.querySelector(".popover-card");
    if (colorValue === 1) {
      topgradient.set(color);
      container.style.setProperty("--top-gradient", color);
    } else if (colorValue === 2) {
      lightbulbscolor.set(color);
      const bulbs = card.querySelectorAll(".bubble");
      bulbs.forEach((bulb) => {
        bulb.style.setProperty("--bulblight", color);

        // if color is the color of the background, add class
        if (color === "white") {
          bulb.classList.add("white");
        } else {
          bulb.classList.remove("white");
        }
      });
    } else if (colorValue === 3) {
      container.style.setProperty("--bottom-gradient", color);
      bottomgradient.set(color);
    }
  }

  function toggleColor(colorValue, color) {
    if (document.startViewTransition) {
      document.startViewTransition(setpropertyofcolor(colorValue, color));
    } else {
      setpropertyofcolor(colorValue, color);
    }
  }

  function createPicture() {
    const card = document.getElementById(`popover-${programLink}-card`);
    const container = card.querySelector(".popover-card");

    // hide every button with cardNumber

    const buttons = card.querySelectorAll(".cardNumber");
    buttons.forEach((button) => {
      button.style.display = "none";
    });

    htmlToImage.toCanvas(container).then((canvas) => {
      // get it inside popover-card
      container.appendChild(canvas);
    });

    // show every button with cardNumber
    buttons.forEach((button) => {
      button.style.display = "block";
    });
  }

  function shareImage() {
    console.log("share image");
    // disable if its not supported

    const card = document.getElementById(`popover-${programLink}-card`);
    const container = card.querySelector(".popover-card");

    const filesArray = [];
    htmlToImage.toBlob(container).then((blob) => {
      filesArray.push(
        new File([blob], `${programName}.png`, { type: blob.type }),
      );
    });

    console.log(navigator);
    if (navigator.canShare && navigator.canShare({ files: filesArray })) {
      navigator
        .share({
          files: filesArray,
          title: "Hier is uw kerstkaart!",
          text: "Veel plezier met uw kerstkaart!",
        })
        .then(() => console.log("Share was successful."))
        .catch((error) => console.log("Sharing failed", error));
    } else {
      console.log(`Your system doesn't support sharing files.`);
    }
  }

  function downloadImage() {
    console.log("download image");

    const card = document.getElementById(`popover-${programLink}-card`);
    const container = card.querySelector(".popover-card");

    htmlToImage.toBlob(container).then((blob) => {
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = `${programName}.png`;
      link.click();
    });
  }

  function closePopover() {
    function closePopover2(card) {
      card.togglePopover();
    }
    const card = document.getElementById(`popover-${programLink}-card`);

    if (document.startViewTransition) {
      document.startViewTransition(closePopover2(card));
    } else {
      closePopover2(card);
    }

    // remove canvas
    const canvas = card.querySelectorAll("canvas");
    canvas.forEach((canvas) => {
      canvas.remove();
    });
  }

  onMount(() => {
    savedCardNumber.subscribe((value) => {
      function gwneenfunctie() {
        Colors = [];
        if (value === 1) {
          Colors = PrimaryColors.map((color) => ({ value: 1, color }));
        } else if (value === 2) {
          Colors = SecondaryColors.map((color) => ({ value: 2, color }));
        } else if (value === 3) {
          Colors = TertiaryColors.map((color) => ({ value: 3, color }));
        }
      }

      if (document.startViewTransition) {
        document.startViewTransition(gwneenfunctie);
      } else {
        gwneenfunctie();
      }
    });
  });

  const firstbutton = 1;
  const thirdbutton = 3;
</script>

<div
  data-sveltekit-preload-data="hover"
  class="popover"
  popover
  id="popover-{programLink}-card"
  style="--vt:{programLink}"
>
  <div class="popover-container">
    <div class="popover-card" id="capture">
      <NumberButton cardNumber={firstbutton} />
      <Fallingsnow />
      <span class="name">Speciaal voor ...</span>
      <span class="title">{programName}</span>
      <Lightbulb />
      <span class="listennow">Luister nu</span>
      <NumberButton cardNumber={thirdbutton} />

      <img
        class="showlogo"
        src="https://fdnd-agency.directus.app/assets/{thumbnailImgSrc}?format=webp"
        alt="logo"
      />

      <img
        class="logo"
        src="https://fdnd-agency.directus.app/assets/{showLogo}?format=webp&height=96&width=96"
        alt="logo"
      />
    </div>

    <div class="popover-menu">
      <button class="button" on:click={() => closePopover()}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M20 4L4 20M4 4L20 20"
            stroke="#FF272A"
            stroke-width="3"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
      <div class="color-picker primary">
        {#each Colors as color (color.color)}
          <button
            style="background: {color.color}"
            on:click={() => toggleColor(color.value, color.color)}
          />
        {/each}
      </div>

      <button class="button check" on:click={() => createPicture()}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <g clip-path="url(#clip0_672_4473)">
            <path
              d="M20 6L9 17L4 12"
              stroke="white"
              stroke-width="3"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </g>
          <defs>
            <clipPath id="clip0_672_4473">
              <rect width="24" height="24" fill="white" />
            </clipPath>
          </defs>
        </svg>
      </button>

      <button class="button share" on:click={() => shareImage()}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M20.7914 12.6075C21.0355 12.3982 21.1575 12.2936 21.2023 12.1691C21.2415 12.0598 21.2415 11.9403 21.2023 11.831C21.1575 11.7065 21.0355 11.6019 20.7914 11.3926L12.3206 4.13202C11.9004 3.77182 11.6903 3.59172 11.5124 3.58731C11.3578 3.58348 11.2101 3.6514 11.1124 3.77128C11 3.90921 11 4.18595 11 4.73942V9.03468C8.86532 9.40813 6.91159 10.4898 5.45971 12.1139C3.87682 13.8846 3.00123 16.176 3 18.551V19.163C4.04934 17.8989 5.35951 16.8766 6.84076 16.166C8.1467 15.5395 9.55842 15.1684 11 15.0706V19.2607C11 19.8141 11 20.0909 11.1124 20.2288C11.2101 20.3487 11.3578 20.4166 11.5124 20.4128C11.6903 20.4084 11.9004 20.2283 12.3206 19.8681L20.7914 12.6075Z"
            stroke="white"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>

      <button class="button save" on:click={() => downloadImage()}>
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M7 3V6.4C7 6.96005 7 7.24008 7.10899 7.45399C7.20487 7.64215 7.35785 7.79513 7.54601 7.89101C7.75992 8 8.03995 8 8.6 8H15.4C15.9601 8 16.2401 8 16.454 7.89101C16.6422 7.79513 16.7951 7.64215 16.891 7.45399C17 7.24008 17 6.96005 17 6.4V4M17 21V14.6C17 14.0399 17 13.7599 16.891 13.546C16.7951 13.3578 16.6422 13.2049 16.454 13.109C16.2401 13 15.9601 13 15.4 13H8.6C8.03995 13 7.75992 13 7.54601 13.109C7.35785 13.2049 7.20487 13.3578 7.10899 13.546C7 13.7599 7 14.0399 7 14.6V21M21 9.32548V16.2C21 17.8802 21 18.7202 20.673 19.362C20.3854 19.9265 19.9265 20.3854 19.362 20.673C18.7202 21 17.8802 21 16.2 21H7.8C6.11984 21 5.27976 21 4.63803 20.673C4.07354 20.3854 3.6146 19.9265 3.32698 19.362C3 18.7202 3 17.8802 3 16.2V7.8C3 6.11984 3 5.27976 3.32698 4.63803C3.6146 4.07354 4.07354 3.6146 4.63803 3.32698C5.27976 3 6.11984 3 7.8 3H14.6745C15.1637 3 15.4083 3 15.6385 3.05526C15.8425 3.10425 16.0376 3.18506 16.2166 3.29472C16.4184 3.4184 16.5914 3.59135 16.9373 3.93726L20.0627 7.06274C20.4086 7.40865 20.5816 7.5816 20.7053 7.78343C20.8149 7.96237 20.8957 8.15746 20.9447 8.36154C21 8.59171 21 8.8363 21 9.32548Z"
            stroke="white"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
    </div>
  </div>
</div>

<style>
  /* Canvas */
  :global(.popover-card canvas) {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  :global(
      .popover-card:has(canvas) .cardNumber,
      .popover-container:has(canvas) .button.check,
      .popover-container:has(canvas) .color-picker
    ) {
    display: none !important;
  }

  :global(
      .popover-container:has(canvas) .button.save,
      .popover-container:has(canvas) .button.share,

    ) {
    display: flex !important;
  }

  /* Edit buttons */
  :global(.popover-card #number-1) {
    top: 1rem;
    left: 85%;
    transform: translateX(-50%);
  }

  :global(.popover-card #number-3) {
    top: calc(100% - 3.5rem);
    left: 48%;
    transform: translateX(-50%);
  }

  /* Card text */

  span {
    position: absolute;
    color: white;
    text-transform: uppercase;
  }

  .name {
    top: 2rem;
    left: 1rem;
    font-size: 1rem;
    font-weight: 500;
    text-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  }

  .title {
    top: 3.7rem;
    left: 1rem;
    font-size: 2.2rem;
    font-weight: 700;
    padding-right: 20px;
    text-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  }

  .listennow {
    top: 17.5rem;
    right: -4rem;
    font-size: 2rem;
    font-weight: 900;
    rotate: -90deg;
  }

  .showlogo {
    border-radius: 99999px;
    position: absolute;
    bottom: 1rem;
    left: -3rem;
    width: 15rem;
    height: 15rem;
    overflow: hidden;
    border: 3px solid white;
    object-fit: cover;
    object-position: center;

    & img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
    }
  }

  .logo {
    position: absolute;
    bottom: 1rem;
    right: 1rem;
    width: 8rem;
    height: 2.5rem;
    overflow: hidden;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    object-position: right;
  }

  /* Popover */

  [popover] {
    z-index: 999;
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    z-index: 1000;
    pointer-events: none;
  }

  .popover-container {
    pointer-events: all;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    gap: 0.5rem;
  }

  .popover-container .popover-card {
    --top-gradient: #37508d;
    --bottom-gradient: #fefefd;
    background: linear-gradient(var(--top-gradient), var(--bottom-gradient));
    transition: 0.3s;
    pointer-events: all;
    border: none;
    border-radius: 12px;
    height: fit-content;
    height: 30rem;
    max-width: 20rem;
    width: 100%;
    border-color: #fff;
    position: relative;
    width: 20rem;
  }

  .popover-container .popover-menu {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }

  .popover-container .popover-menu > button,
  .popover-container .popover-menu > div {
    background: white;
    padding: 10px;
    display: grid;
    place-items: center;

    width: 3.5rem;
    border: none;
    border-radius: 12px;
  }

  .popover-menu > button.save,
  .popover-menu > button.share {
    display: none;
    background: #2ebf61;
    transition: 0.1s;

    &:hover {
      background: #238545 !important;
      transition: 0.1s;
    }
  }

  .popover-menu > button.check {
    background: #2ebf61;
    transition: 0.1s;

    &:hover {
      background: #238545 !important;
      transition: 0.1s;
    }
  }

  .popover-container:has(canvas) .popover-menu > button.save,
  .popover-container:has(canvas) .popover-menu > button.share {
    display: grid;
  }

  .popover-container .popover-menu > .button {
    height: 3.5rem;
    cursor: pointer;
    &:hover {
      background: #e4e4e4;
    }
  }

  .popover-container .popover-menu .color-picker {
    display: flex;
    align-items: center;
    justify-items: center;
    flex-direction: column;
    gap: 0.5rem;
    padding: 10px;
    height: fit-content;
    min-height: 3.5rem;
    view-transition-name: colorpicker;
  }

  .color-picker button {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    aspect-ratio: 1 / 1;
    border: none;
    cursor: pointer;
    transition: 0.3s;

    &:hover {
      filter: brightness(80%);
      transition: 0.3s;
    }

    &:active {
      filter: brightness(40%);
      transition: 0.3s;
    }
  }

  /* in card elements */
  .popover-card {
    position: relative;
    overflow: hidden;
  }
</style>
