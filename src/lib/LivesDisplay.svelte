<script>
  export let livesLeft;
  export let status;
</script>

<div class="livesContainer">
  {#if status == "play"}
    {#each Array(livesLeft) as _, index (index)}
      <span id="hearts">&#9829;</span>
    {/each}
  {:else if status == "lost"}
    You loose! 😬
  {:else}
    You won! 🏆
  {/if}
</div>

<style>
  .livesContainer {
    font-size: 100px;
    grid-area: hangman;
    color: var(--yellow);
  }
  #hearts {
    font-size: 80px;
    color: var(--purple);
  }
</style>
