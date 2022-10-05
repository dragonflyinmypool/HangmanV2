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
    gameStage: 'play',
    livesLeft:0,
    word:[],
    pickedLetters:[],
    wordTogether:""
  }
 
  function newGame() {
    let livesLeft = Number(settings.totalLives)
    // Pick the word, and format into arrays
    let [word,wordTogether] = getRandomWord(settings.currentCatagory)
    // Reset the game vaible/state


    state = resetState(livesLeft, getRandomWord(settings.currentCatagory));
  }
  
  function resetState(livesLeft, word, wordTogether){ 
    console.log(livesLeft, word, wordTogether)
    return {
      // Possible statuses: play, lost, won
      gameStage:'play',
      livesLeft:livesLeft,
      word:word,
      wordTogether:wordTogether,
      pickedLetters:[],
    }
  }

  function getRandomWord(catagory) {
    // Go to current catagory word list and get a random word
    let currentWordList = wordList.words[catagory];
    let word = currentWordList[Math.floor(Math.random() * currentWordList.length)]
    let wordTogether = word.replace(/\s/g, '')

    // Proccess the word (creates an array for each word, and an entry for each letter)
    word = word.toUpperCase().split(" ").map((element) => element.split(""));

    console.log(word, wordTogether)
    return { word, wordTogether};
  }

  newGame();

  // GAME PLAY
  // Handle letter click
  function letterClick(e) {
    function checkPicked(letter) {
      return !pickedLetters.includes(letter);
    }

    // Update letter lists
    state.pickedLetters.push(e.detail);

    console.log(state, state.livesLeft)
    // Update lives
    state.livesLeft = state.word.includes(e.detail) ? state.livesLeft : state.livesLeft - 1;

    // Check for game over
    if (state.livesLeft < 1) {
      status = "lost";
    }

    // let currentWord = state.word
    // console.log(state.word)

    // // let lettersWithoutSpaces = currentWord.replace(/,/g,"");
    // // console.log(state.word, lettersWithoutSpaces)

    // // // let checker = (arr, target) => target.every((v) => arr.includes(v));

    // // // if (checker(state.pickedLetters, lettersWithoutSpaces)) {
    // // //   status = "won";
    // // // }

  }
</script>

<main>
  <WordDisplay word={state.word} pickedLetters={state.pickedLetters} status={state.gameStage} />
  <div class="flex">
    <Keyboard pickedLetters={state.pickedLetters} status={state.gameStage} on:letterClick={letterClick}/>
    <LivesDisplay livesLeft={state.livesLeft} status={state.gameStage} />
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
    grid-template-columns: 1000px 500px;
    grid-template-areas: "keyboard hangman";
  }
</style>
