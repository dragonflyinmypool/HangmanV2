<script>
  import Prompt from "./lib/Prompt.svelte";
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Menu from "./lib/Menu.svelte";
  import HangmanAnimation from "./lib/HangmanAnimation.svelte";
  import Keyboard2 from "./lib/Keyboard2.svelte";
  import item from "./assets/wordList.json";

  // GAME SETUP

  // Current settings
  let settings = {
    lives: ["1", "2", "3", "4", "5", "6", "7"],
    totalLives: "5",
    catagories: ["Animals", "Dog Breeds", "Insects"],
    currentCatagory: "Dog Breeds",
  };

  // Content data
  let words;
  let curentTopic;
  let word;

  // Status
  // possible statuses: play, lost, won
  let status;
  // Game variables
  let pickedLetters = [];
  let splitByWord;
  let eachWordSplit;
  let allLetters;
  let livesLeft;

  function newGame() {
    status = "play";
    livesLeft = Number(settings.totalLives);
    pickedLetters = [];

    curentTopic = settings.currentCatagory;
    settings = settings;

    // Pick the word
    words = item.words;
    let currentWordList = words[curentTopic];
    word = currentWordList[Math.floor(Math.random() * currentWordList.length)];
    word = word.toUpperCase();

    // Proccess the word
    splitByWord = word.split(" ");
    eachWordSplit = splitByWord.map((element) => element.split(""));

    // Keyboard
    allLetters = [...Array(26)].map((_, i) =>
      String.fromCharCode(i + 97).toUpperCase()
    );
  }
  newGame();

  // GAME PLAY
  // Handle letter click
  function letterClick(e) {
    // Update letter list
    pickedLetters.push(e.detail);
    allLetters = allLetters;
    eachWordSplit = eachWordSplit;

    // Update lives
    let theLettersSplit = word.split("");
    livesLeft = theLettersSplit.includes(e.detail) ? livesLeft : livesLeft - 1;

    // Check for game over
    if (livesLeft < 1) {
      status = "lost";
    }

    // // Check for win
    let lettersWithoutSpaces = word.replace(" ", "").replace(" ", "").split("");
    let checker = (arr, target) => target.every((v) => arr.includes(v));
    if (checker(pickedLetters, lettersWithoutSpaces)) {
      status = "won";
    }
  }
</script>

<main>
  <WordDisplay {eachWordSplit} {pickedLetters} {status} />
  <div class="flex">
    <Keyboard2
      {allLetters}
      {pickedLetters}
      {status}
      on:letterClick={letterClick}
    />
    <HangmanAnimation {livesLeft} {status} />
  </div>
  <Menu on:newGame={newGame} {settings} />
</main>

<style>
  main {
    width: 1900px;
    display: grid;
    justify-content: center;
    align-items: center;
    grid-template-rows: 500px 280px;
    row-gap: 30px;
  }
  .flex {
    width: 1700px;
    display: grid;
    grid-template-columns: 300px 1000px 300px;
    grid-template-areas: ". keyboard hangman";
  }
</style>
