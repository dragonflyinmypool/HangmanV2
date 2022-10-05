<script>
  export let word = [];
  export let pickedLetters;
  export let status;
</script>

<div id="container">
  {#each word as currentWord, i}
    <div class="line">
      {#each currentWord as letter}
        <div class="letter">
          {pickedLetters.includes(letter) || status == "lost" ? letter : ""}
        </div>
      {/each}
    </div>
  {/each}
</div>

<style>
  #container {
    min-height: 120px;
    display: grid;
    justify-content: left;
    align-items: center;
  }
  .line {
    display: flex;
    flex-wrap: wrap;
    align-content: center;
    justify-content: left;
    box-shadow: none;
    margin-bottom: 7px;
  }
  .letter {
    width: 120px;
    height: 120px;
    font-size: 110px;
    line-height: 120px;
    text-align: center;
    font-weight: bold;
    background-color: var(--purple);
    border: var(--lightBlue) 2px solid;
    color: var(--yellow);
  }
</style>
