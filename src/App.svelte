<script>
  import Prompt from "./lib/Prompt.svelte";
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Menu from "./lib/Menu.svelte";
  import HangmanAnimation from "./lib/HangmanAnimation.svelte";
  import KeyboardL from "./lib/KeyboardL.svelte";

  let catagories = ["US History", "US Presidents", "Famous landmarks"];
</script>

<main>
  <Prompt>{catagories[0]}</Prompt>
  <HangmanAnimation />
  <WordDisplay />
  <KeyboardL />
  <Menu />
</main>

<style>
  main {
    display: grid;
    justify-content: center;
  }
</style>
