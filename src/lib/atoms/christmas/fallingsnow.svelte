<script>
  import { onMount } from "svelte";

  onMount(() => {
    const circles = document.querySelectorAll("circle");
    circles.forEach((circle, index) => {
      circle.style.animationDelay = `${Math.random() * 6}s`;
      circle.style.animationDuration = `${Math.random() * 6 + 5}s`;
    });
  });
</script>

<svg
  class="snow"
  width="225"
  height="393"
  viewBox="0 0 225 393"
  fill="none"
  xmlns="http://www.w3.org/2000/svg"
>
  <circle cx="219.133" cy="71.2289" r="2.95203" fill="white" />
  <circle cx="225.037" cy="305.915" r="2.95203" fill="white" />
  <circle cx="146.808" cy="119.937" r="2.95203" fill="white" />
  <circle cx="152.712" cy="350.196" r="2.95203" fill="white" />
  <circle cx="185.184" cy="186.358" r="2.95203" fill="white" />
  <circle cx="40.535" cy="226.21" r="2.95203" fill="white" />
  <circle cx="161.568" cy="9.23621" r="2.95203" fill="white" />
  <circle cx="5.11072" cy="208.498" r="2.95203" fill="white" />
  <circle cx="73.0072" cy="341.339" r="2.95203" fill="white" />
  <circle cx="171.9" cy="319.199" r="2.95203" fill="white" />
  <circle cx="99.5756" cy="367.908" r="2.95203" fill="white" />
  <circle cx="65.6273" cy="217.354" r="2.95203" fill="white" />
  <circle cx="-0.793088" cy="40.2325" r="2.95203" fill="white" />
  <circle cx="205.849" cy="150.933" r="2.95203" fill="white" />
  <circle cx="78.9115" cy="252.779" r="2.95203" fill="white" />
  <circle cx="212.491" cy="162.004" r="0.738007" fill="white" />
  <circle cx="27.989" cy="38.0185" r="0.738007" fill="white" />
  <circle cx="87.0295" cy="263.849" r="0.738007" fill="white" />
  <circle cx="61.9372" cy="38.0185" r="0.738007" fill="white" />
  <circle cx="23.5608" cy="69.0149" r="0.738007" fill="white" />
  <circle cx="166.734" cy="24.7343" r="0.738007" fill="white" />
  <circle cx="107.694" cy="193" r="0.738007" fill="white" />
  <circle cx="125.406" cy="268.277" r="0.738007" fill="white" />
  <circle cx="190.35" cy="86.727" r="0.738007" fill="white" />
  <circle cx="143.118" cy="7.02219" r="0.738007" fill="white" />
  <circle cx="25.0368" cy="272.705" r="0.738007" fill="white" />
  <circle cx="95.8855" cy="170.86" r="0.738007" fill="white" />
  <circle cx="213.967" cy="51.3025" r="0.738007" fill="white" />
  <circle cx="32.4172" cy="259.421" r="0.738007" fill="white" />
  <circle cx="109.17" cy="148.719" r="0.738007" fill="white" />
  <circle cx="106.217" cy="64.5866" r="0.738007" fill="white" />
  <circle cx="200.683" cy="162.004" r="0.738007" fill="white" />
  <circle cx="156.402" cy="259.421" r="0.738007" fill="white" />
  <circle cx="104.742" cy="321.413" r="0.738007" fill="white" />
  <circle cx="168.211" cy="268.277" r="0.738007" fill="white" />
  <circle cx="45.7014" cy="365.694" r="0.738007" fill="white" />
  <circle cx="29.4651" cy="86.727" r="0.738007" fill="white" />
  <circle cx="181.494" cy="38.0185" r="0.738007" fill="white" />
  <circle cx="57.509" cy="86.727" r="0.738007" fill="white" />
  <circle cx="16.1809" cy="7.02219" r="0.738007" fill="white" />
  <circle cx="115.074" cy="201.856" r="0.738007" fill="white" />
  <circle cx="134.262" cy="277.133" r="0.738007" fill="white" />
  <circle cx="26.5129" cy="254.993" r="0.738007" fill="white" />
  <circle cx="103.265" cy="139.863" r="0.738007" fill="white" />
  <circle cx="215.443" cy="20.3064" r="0.738007" fill="white" />
  <circle cx="47.177" cy="263.849" r="0.738007" fill="white" />
  <circle cx="116.55" cy="162.004" r="0.738007" fill="white" />
  <circle cx="131.31" cy="86.727" r="0.738007" fill="white" />
  <circle cx="44.2253" cy="170.86" r="0.738007" fill="white" />
  <circle cx="209.539" cy="210.712" r="0.738007" fill="white" />
  <circle cx="82.6013" cy="20.3064" r="0.738007" fill="white" />
  <circle cx="137.214" cy="250.565" r="0.738007" fill="white" />
  <circle cx="33.8928" cy="91.155" r="0.738007" fill="white" />
  <circle cx="191.826" cy="51.3025" r="0.738007" fill="white" />
  <circle cx="126.882" cy="210.712" r="0.738007" fill="white" />
  <circle cx="8.80051" cy="210.712" r="0.738007" fill="white" />
  <circle cx="30.9411" cy="321.413" r="0.738007" fill="white" />
  <circle cx="141.642" cy="316.985" r="0.738007" fill="white" />
  <circle cx="35.3694" cy="259.421" r="0.738007" fill="white" />
  <circle cx="112.122" cy="153.148" r="0.738007" fill="white" />
  <circle cx="138.69" cy="113.295" r="0.738007" fill="white" />
  <circle cx="58.9851" cy="104.439" r="0.738007" fill="white" />
  <circle cx="211.014" cy="64.5866" r="0.738007" fill="white" />
  <circle cx="135.738" cy="219.568" r="0.738007" fill="white" />
  <circle cx="36.8449" cy="356.838" r="0.738007" fill="white" />
  <circle cx="113.598" cy="294.845" r="0.738007" fill="white" />
  <circle cx="60.4616" cy="223.996" r="0.738007" fill="white" />
  <circle cx="69.3171" cy="325.841" r="0.738007" fill="white" />
  <circle cx="202.158" cy="316.985" r="0.738007" fill="white" />
  <circle cx="48.653" cy="268.277" r="0.738007" fill="white" />
  <circle cx="123.93" cy="162.004" r="0.738007" fill="white" />
  <circle cx="157.878" cy="162.004" r="0.738007" fill="white" />
  <circle cx="85.5534" cy="193" r="0.738007" fill="white" />
  <circle cx="128.358" cy="24.7343" r="0.738007" fill="white" />
  <circle cx="199.207" cy="259.421" r="0.738007" fill="white" />
  <circle cx="50.1291" cy="277.133" r="0.738007" fill="white" />
  <circle cx="84.0779" cy="108.867" r="0.738007" fill="white" />
  <circle cx="165.259" cy="223.996" r="0.738007" fill="white" />
  <circle cx="88.5056" cy="259.421" r="0.738007" fill="white" />
  <circle cx="188.875" cy="339.125" r="0.738007" fill="white" />
  <circle cx="140.166" cy="392.262" r="0.738007" fill="white" />
  <circle cx="110.646" cy="339.125" r="0.738007" fill="white" />
  <circle cx="129.834" cy="268.277" r="0.738007" fill="white" />
</svg>

<style>
  .snow {
    position: absolute;
    height: 100%;
    width: 100%;
    inset: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden; /* Ensures snowflakes are contained */
  }

  circle {
    opacity: 0;
    animation: appearAndFall 15s linear infinite;
  }

  @keyframes appearAndFall {
    0% {
      opacity: 0;
      transform: translateY(-40%);
    }
    10% {
      opacity: 1;
    }
    90% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      transform: translateY(100%);
    }
  }
</style>
