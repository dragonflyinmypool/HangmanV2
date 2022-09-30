<script>
  export let eachWordSplit = [];
  for (let index = 0; index < eachWordSplit.length; index++) {
    const element = eachWordSplit[index];
  }
</script>

<div id="container">
  {#each eachWordSplit as word, i}
    <div class="line">
      {#each eachWordSplit[i] as letter}
        <div class="letter">{letter}</div>
      {/each}
    </div>
  {/each}
</div>

<style>
  .line {
    display: flex;
    align-content: center;
    justify-content: center;
    box-shadow: none;
    margin-bottom: 7px;
  }
  .letter {
    width: 23px;
    height: 30px;
    font-size: 20px;
    line-height: 30px;
    text-align: center;
    font-weight: bold;
  }
</style>
