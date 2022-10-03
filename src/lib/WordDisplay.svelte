<script>
  export let eachWordSplit = [];
  export let pickedLetters;
  export let status;

  // Set up display
  for (let index = 0; index < eachWordSplit.length; index++) {
    const element = eachWordSplit[index];
  }
</script>

<div id="container">
  {#each eachWordSplit as word, i}
    <div class="line">
      {#each eachWordSplit[i] as letter}
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
    justify-content: center;
    align-items: center;
  }
  .line {
    display: flex;
    align-content: center;
    justify-content: center;
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
  }
</style>
