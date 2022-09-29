<script>
  export let wordSplit = "";
</script>

<div class="line">
  {#each wordSplit as letter}
    <div class="letter">{letter}</div>
  {/each}
</div>

<style>
  .line {
    display: flex;
    align-content: center;
    justify-content: center;
    box-shadow: none;
  }
  .letter {
    border: solid 2px white;
    width: 30px;
    height: 35px;
    font-size: 30px;
    text-align: center;
    background-color: blueviolet;
    color: white;
  }
</style>
