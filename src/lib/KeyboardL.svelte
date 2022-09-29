<script>
  export let allLetters;
  export let pickedLetters;
</script>

<div class="keyboard">
  {#each allLetters as letter, i}
    <div class="letter">{letter}</div>
  {/each}
</div>

<style>
  .keyboard {
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(7, 40px);
    grid-template-rows: repeat(4, 60px);
    justify-content: center;
  }
  .letter {
    height: 30px;
    width: 30px;
    background-color: transparent;
    /* border: 1px solid black; */
    padding: 0px;
    text-align: center;
  }
</style>
