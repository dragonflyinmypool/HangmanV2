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
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }
  .kLetter {
    width: 40px;
    height: 40px;
    text-align: center;
    line-height: 40px;
    font-weight: bold;
    font-size: 30px;
  }
  .unpicked {
    font-weight: 100;
  }
  button {
    border: none;
    border-radius: 20%;
  }
</style>
