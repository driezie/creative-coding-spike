<script>
  import { savedCardNumber } from "$lib/stores/cardStore";
  export let cardNumber = 1;
  export let selected = false;

  savedCardNumber.subscribe((value) => {
    selected = value === cardNumber;
  });

  export function buttonClick() {
    savedCardNumber.set(cardNumber);
    console.log("button clicked with number: ", cardNumber);
  }
</script>

<button
  class="cardNumber {selected ? 'selected' : ''}"
  id="number-{cardNumber}"
  on:click={buttonClick}
>
  {cardNumber}
</button>

<style>
  button {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    background: transparent;
    border: none;
    width: 2.5rem;
    height: 2.5rem;
    pointer-events: all;
    align-items: center;
    display: flex;
    justify-content: center;
    font-family: var(--font-family);
    font-weight: 500;
    aspect-ratio: 1/1;
    background-color: white;
    color: black;
    border-radius: 50%;

    font-size: 1rem;
    margin: 0 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    z-index: 100;
    transition: 0.2s;
    cursor: pointer;
    animation: fadeIn 1s alternate ease-in-out forwards;

    &.selected {
      background-color: #ababab;
    }

    &:hover {
      background-color: #ababab;
      transition: 0.2s;
    }
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
