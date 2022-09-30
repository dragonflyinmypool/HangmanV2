<script>
  export let allLetters;
  export let pickedLetters;

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function disableKeys(letter) {
    // allLetters = allLetters;
    return pickedLetters.includes(letter) ? true : false;
  }
</script>

<div class="keyboard">
  {#each allLetters as letter}
    <button
      disabled={disableKeys(letter)}
      class="kLetter"
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
  }
</style>
