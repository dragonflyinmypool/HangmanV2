<script>
  import Prompt from "./lib/Prompt.svelte";
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Menu from "./lib/Menu.svelte";
  import HangmanAnimation from "./lib/HangmanAnimation.svelte";
  import Keyboard2 from "./lib/Keyboard2.svelte";

  // Content data
  let catagories = ["US History", "US Presidents", "Famous landmarks"];
  let word = "ABRAHAM LINCOLN";

  // Proccess the word
  let splitByWord = word.split(" ");
  let eachWordSplit = splitByWord.map(function (element) {
    return element.split("");
  });

  let wordSplit = ["a", "b"];
  // Keyboard
  let allLetters = [...Array(26)].map((_, i) =>
    String.fromCharCode(i + 97).toUpperCase()
  );

  let pickedLetters = [];

  function letterClick(e) {
    pickedLetters.push(e.detail);
    allLetters = allLetters;
  }
</script>

<main>
  <Prompt>{catagories[0]}</Prompt>
  <HangmanAnimation />
  <WordDisplay {eachWordSplit} />
  <Keyboard2 {allLetters} {pickedLetters} on:letterClick={letterClick} />
  <Menu />
</main>

<style>
  main {
    display: grid;
    justify-content: center;
    align-items: center;
    row-gap: 15px;
  }
</style>
