<script>
  import { onMount } from "svelte";

  let number = 2;
  import NumberButton from "$lib/atoms/numberButton.svelte";

  onMount(() => {
    const ellipses = document.querySelectorAll("ellipse");
    ellipses.forEach((ellipse) => {
      ellipse.style.animationDelay = `${Math.random() * 6}s`;
      ellipse.style.animationDuration = `${Math.random() * 6 + 5}s`;
    });
  });
</script>

<NumberButton cardNumber={number} />

<svg
  class="lightbulbs"
  width="225"
  height="54"
  viewBox="0 0 225 54"
  fill="none"
  xmlns="http://www.w3.org/2000/svg"
>
  <path
    d="M244.948 0.031509C244.964 4.61019 241.549 9.15599 234.899 13.4094C228.25 17.6627 218.495 21.5404 206.191 24.8209C193.888 28.1014 179.278 30.7206 163.194 32.5288C147.11 34.337 129.869 35.299 112.453 35.3596C95.0381 35.4203 77.7902 34.5786 61.6944 32.8824C45.5986 31.1863 30.9702 28.669 18.6444 25.4743C6.31865 22.2796 -3.46314 18.47 -10.1424 14.2631C-16.8217 10.0561 -20.2677 5.53425 -20.2837 0.955566"
    stroke="black"
  />
  <rect
    x="14.3022"
    y="22.8948"
    width="6.82607"
    height="10.1336"
    rx="3.41303"
    transform="rotate(16.6792 14.3022 22.8948)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="14.2088"
    cy="35.484"
    rx="6.59203"
    ry="6.59203"
    transform="rotate(16.6793 14.2088 35.484)"
    fill="white"
  />
  <rect
    x="52.5732"
    y="30.4709"
    width="6.82607"
    height="10.1336"
    rx="3.41303"
    transform="rotate(7.36949 52.5732 30.4709)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="54.5182"
    cy="42.9095"
    rx="6.59203"
    ry="6.59203"
    transform="rotate(7.36949 54.5182 42.9095)"
    fill="white"
  />
  <rect
    x="89.2886"
    y="34.2954"
    width="6.82606"
    height="10.1336"
    rx="3.41303"
    transform="rotate(1.40426 89.2886 34.2954)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="92.5154"
    cy="46.4645"
    rx="6.59203"
    ry="6.59203"
    transform="rotate(1.40426 92.5154 46.4645)"
    fill="white"
  />
  <rect
    x="125.578"
    y="34.5847"
    width="6.82607"
    height="10.1336"
    rx="3.41304"
    transform="rotate(-5.09896 125.578 34.5847)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="130.162"
    cy="46.3101"
    rx="6.59204"
    ry="6.59203"
    transform="rotate(-5.09896 130.162 46.3101)"
    fill="white"
  />
  <rect
    x="165.882"
    y="32.1919"
    width="6.82606"
    height="10.1336"
    rx="3.41303"
    transform="rotate(-11.6022 165.882 32.1919)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="171.765"
    cy="43.3225"
    rx="6.59203"
    ry="6.59203"
    transform="rotate(-11.6022 171.765 43.3225)"
    fill="white"
  />
  <rect
    x="205.614"
    y="24.4473"
    width="6.82607"
    height="10.1336"
    rx="3.41303"
    transform="rotate(-18.1054 205.614 24.4473)"
    fill="#0F2672"
  />
  <ellipse
    class="bubble"
    cx="212.72"
    cy="34.8399"
    rx="6.59203"
    ry="6.59203"
    transform="rotate(-18.1054 212.72 34.8399)"
    fill="white"
  />
</svg>

<style>
  :global(.cardNumber) {
    left: 1rem;
    top: 12rem;
  }

  .lightbulbs {
    position: absolute;
    height: 20rem;
    width: 100%;
  }

  .lightbulbs .bubble {
    --bulblight: white;
    fill: var(--bulblight);
    view-transition-name: pickerchange;
  }
</style>
