<script>
  export let options;
  export let currentOption;

  console.log(options);
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
  select {
    border: none;
    border-radius: 5px;
    font-size: 17px;
    padding: 0.5px;
    min-width: 100px;
  }
  option {
    background-color: #ffffff29;
  }
</style>
