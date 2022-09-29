<script>
  import Prompt from "./lib/Prompt.svelte";
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Menu from "./lib/Menu.svelte";
  import HangmanAnimation from "./lib/HangmanAnimation.svelte";
  import KeyboardL from "./lib/KeyboardL.svelte";

  let catagories = ["US History", "US Presidents", "Famous landmarks"];
  let word = "LINCOLN";
  let wordSplit = word.split("");

  // Keyboard
  let allLetters = [...Array(26)].map((_, i) =>
    String.fromCharCode(i + 97).toUpperCase()
  );
  let pickedLetters = [];
</script>

<div>
  <main>
    <Prompt>{catagories[0]}</Prompt>
    <HangmanAnimation />
    <WordDisplay {wordSplit} />
    <KeyboardL {allLetters} {pickedLetters} />
    <Menu />
  </main>
</div>

<style>
  main {
    width: 95%;
    display: grid;
    justify-content: center;
    align-items: center;
    grid-template-rows: 20px 200px 150px 250px;
  }
</style>
