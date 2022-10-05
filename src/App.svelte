<script>
  // Import components
  import WordDisplay from "./lib/WordDisplay.svelte";
  import Menu from "./lib/Menu.svelte";
  import LivesDisplay from "./lib/LivesDisplay.svelte";
  import Keyboard from "./lib/Keyboard.svelte";
  import wordList from "./assets/wordList.json";

  // GAME SETUP
  // Current settings
  let settings = {
    lives: ["1", "2", "3", "4", "5", "6", "7"],
    totalLives: "5",
    catagories: ["Animals", "Dog Breeds", "Insects"],
    currentCatagory: "Dog Breeds",
  };

  // State
  let state = {
    gameStage: "play",
    livesLeft: 0,
    word: [],
    pickedLetters: [],
    wordTogether: "",
    allLetters: [],
    nextLetter: 0,
  };

  // NEW GAME
  function newGame() {
    let livesLeft = Number(settings.totalLives);

    // Pick the word, and format into arrays
    let [word, wordTogether] = getRandomWord(settings.currentCatagory);

    let allLetters = [...Array(26)].map((_, i) =>
      String.fromCharCode(i + 97).toUpperCase()
    );

    // Reset the game vaible/state
    state = resetState(livesLeft, word, wordTogether, allLetters);
  }

  function resetState(livesLeft, word, wordTogether, allLetters) {
    return {
      // Possible statuses: play, lost, won
      gameStage: "play",
      livesLeft: livesLeft,
      word: word,
      wordTogether: wordTogether,
      pickedLetters: [],
      allLetters: allLetters,
      nextLetter: 0,
    };
  }

  function getRandomWord(catagory) {
    // Go to current catagory word list and get a random word
    let currentWordList = wordList.words[catagory];
    let word =
      currentWordList[Math.floor(Math.random() * currentWordList.length)];
    let wordTogether = word.replace(/\s/g, "").toUpperCase();

    // Proccess the word (creates an array for each word, and an entry for each letter)
    word = word
      .toUpperCase()
      .split(" ")
      .map((element) => element.split(""));

    return [word, wordTogether];
  }

  newGame();

  let newGameButton;
  // GAME PLAY
  // Handle letter click
  function letterClick(e) {
    // Update letter lists
    state.pickedLetters.push(e.detail.letter);
    state.pickedLetters = state.pickedLetters;

    updateLives(e);
    updateFocus(e.detail);
  }

  function updateLives(e) {
    // Update lives
    state.livesLeft = state.wordTogether.includes(e.detail.letter)
      ? state.livesLeft
      : state.livesLeft - 1;

    // Check for game over
    if (state.livesLeft < 1) {
      state.gameStage = "lost";
      newGameButton.focus();
    }

    // Check if game has been won
    let checker = (arr, target) => target.every((v) => arr.includes(v));

    if (checker(state.pickedLetters, state.wordTogether.split(""))) {
      newGameButton.focus();
      state.gameStage = "won";
    }
  }
  function updateFocus(e) {
    let unpickedLetters = state.allLetters.filter(checkPicked);
    function checkPicked(keyboardLetter) {
      return !state.pickedLetters.includes(keyboardLetter);
    }

    state.nextLetter = findNextLetter();

    function findNextLetter() {
      let nextLetter;
      for (var i = 0; i < state.allLetters.length; i++) {
        if (e.id < i && checkPicked(state.allLetters[i])) {
          return i;
        }
      }

      for (var i = 0; i < state.allLetters.length; i++) {
        if (checkPicked(state.allLetters[i])) {
          return i;
        }
      }
    }
  }
</script>

<main>
  <WordDisplay
    word={state.word}
    pickedLetters={state.pickedLetters}
    status={state.gameStage}
  />
  <div class="flex">
    <Keyboard
      pickedLetters={state.pickedLetters}
      status={state.gameStage}
      allLetters={state.allLetters}
      nextLetter={state.nextLetter}
      on:letterClick={letterClick}
    />
    <LivesDisplay livesLeft={state.livesLeft} status={state.gameStage} />
  </div>
  <Menu on:newGame={newGame} {settings} bind:newGameButton />
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
    grid-template-columns: 1000px 500px;
    grid-template-areas: "keyboard hangman";
  }
</style>
