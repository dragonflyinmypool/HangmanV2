<script>
  export let allLetters;
  export let pickedLetters;
  export let status;

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function disableKeys(letter) {
    if (status == "lost" || status == "won") {
      return true;
    }
    return pickedLetters.includes(letter);
  }
</script>

<div class="keyboard">
  {#each allLetters as letter}
    <button
      disabled={disableKeys(letter)}
      class="kLetter"
      class:unpicked={disableKeys(letter)}
      on:click={() => {
        dispatch("letterClick", letter);
      }}
    >
      {letter}
    </button>
  {/each}
</div>

<style>
  .keyboard {
    max-width: 830px;
    display: grid;
    grid-template-columns: repeat(9, 70px);
    gap: 20px;
    grid-area: keyboard;
  }
  .kLetter {
    width: 70px;
    height: 70px;
    text-align: center;
    line-height: 70px;
    font-weight: bold;
    font-size: 60px;
  }
  .unpicked {
    font-weight: 100;
  }
  button {
    border: none;
    border-radius: 20%;
  }
</style>
