<script>
  import Prompt from "./lib/Prompt.svelte";
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Letters from "./lib/Letters.svelte";
  import Menu from "./lib/Menu.svelte";
  import HangmanAnimation from "./lib/HangmanAnimation.svelte";
</script>

<h1>Hangman Game</h1>
<Prompt />
<HangmanAnimation />
<WordDisplay />
<Letters />
<Menu />
