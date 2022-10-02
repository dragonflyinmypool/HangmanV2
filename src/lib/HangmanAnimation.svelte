<script>
  export let livesLeft;
  export let status;
</script>

<div class="livesContainer">
  {#if status == "play"}
    {#each Array(livesLeft) as _, index (index)}
      &#9829;
    {/each}
  {:else if status == "lost"}
    You loose! 😬
  {:else}
    You won! 🏆
  {/if}
</div>

<style>
  .livesContainer {
    font-size: 25px;
  }
</style>
