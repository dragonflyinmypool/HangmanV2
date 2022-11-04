<script>
  export let options;
  export let currentOption;
</script>

<div>
  <slot />
  <select value={currentOption} on:change>
    {#each options as option}
      <option value={option}>
        {option}
      </option>
    {/each}
  </select>
</div>

<style>
  div {
    font-size: 40px;
  }
  select {
    border: none;
    border-radius: 5px;
    font-size: 40px;
    padding: 10px;
    min-width: 100px;
    background-color: var(--purple);
    color: var(--lightBlue);
    text-align: center;
    border-radius: 10px;
  }
  option {
    background-color: #ffffff29;
  }
</style>
