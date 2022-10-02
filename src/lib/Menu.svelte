<script>
  import { createEventDispatcher } from "svelte";
  import SelectButton from "./SelectButton.svelte";
  export let settings;

  let dispatch = createEventDispatcher();

  function newGame() {
    dispatch("newGame");
  }
  function changeCatagory(e) {
    settings.currentCatagory = e.target.value;
    settings = settings;
    newGame();
  }

  function changeLives(e) {
    settings.totalLives = e.target.value;
    settings = settings;
    newGame();
  }
</script>

<div id="container">
  <button>Hint</button>
  <SelectButton
    options={settings.catagories}
    currentOption={settings.currentCatagory}
    on:change={changeCatagory}
  />
  <button on:click={newGame}>New Game</button>
  <SelectButton
    options={settings.lives}
    currentOption={settings.totalLives}
    on:change={changeLives}>Lives:</SelectButton
  >
</div>

<style>
  #container {
    min-height: 100px;
    display: grid;
    gap: 18px;
    align-items: center;
    align-content: center;
    justify-content: center;
    grid-template-columns: 100px 150px;
    padding: 20px;
  }
  button {
    font-size: 17px;
  }
</style>
