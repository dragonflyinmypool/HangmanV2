<script>
  // Import dependencies
  import { onMount, afterUpdate } from 'svelte';

  import { createEventDispatcher } from "svelte";

  export let pickedLetters;
  export let status;
  export let allLetters;
  export let nextLetter;
  
  const dispatch = createEventDispatcher();

  let keyboard
  let keyboardChildren;

  
  $:{
    pickedLetters = pickedLetters
    allLetters = allLetters
  }


  afterUpdate(() => {
    let keyboardChildren = keyboard.childNodes
    if (pickedLetters.length > 0) {
      keyboardChildren[nextLetter].focus()
    }
  });

  function disableKeys(letter) {
    if (status == "lost" || status == "won") {
      return true;
    }
    return pickedLetters.includes(letter);
  }

  // Focus
  onMount(() => {
    keyboard.firstChild.focus()
  });

  function keyClick(letter, id) {
    dispatch('letterClick',{
      letter:letter,
      id:id
    })
  }
</script>

<div class="keyboard" bind:this={keyboard}>
  {#each allLetters as letter, id}
    <button
      disabled={disableKeys(letter)}
      class="kLetter"
      class:unpicked={disableKeys(letter)}
      on:click={keyClick(letter, id)}
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
    background-color: var(--purple);
    color: var(--lightBlue);
  }
  .unpicked {
    font-weight: 100;
    color: var(--purple);
    background-color: #8e55a334;
    color: #8e55a331;
  }
  button {
    border: none;
    border-radius: 20%;
    color: var(--red);
  }
</style>
