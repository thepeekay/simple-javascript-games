1. **Define the game data:**
* Define an array of words to be used in the game.
* Define the number of allowed guesses (lives) for the player.
2. **Select a word:**
* Select a random word from the array of words.
* Create an array to represent the current state of the word, with each letter replaced by a blank _.
3. **Render the game UI:**
* Create a container element for the game.
* Display the current state of the word, with blank spaces for each letter.
* Display the number of remaining lives.
* Add an input field for the player to enter a letter.
4. **Handle player input:**
* Add an event listener to the input field to listen for when the player enters a letter.
* When a letter is entered, check if it matches any letters in the selected word.
* If the letter matches, reveal the corresponding letter in the current state of the word.
* If the letter does not match, decrement the number of remaining lives.
5. **Check for game over:**
* Check if the player has guessed all the letters in the selected word.
* If the player has guessed all the letters, display a message indicating that they have won.
* If the player has run out of lives, display a message indicating that they have lost.
6. **Restart the game:**
* Add a restart button to the game UI.
* When the restart button is clicked, select a new word and reset the game state.

## 1 - Define game data

1. Define an array of words to be used in the game: You can create an array of words that will be randomly selected for the player to guess. These words can be of varying lengths and difficulty levels.
```js
let words = ['javascript', 'python', 'html', 'css', 'react', 'angular', 'vue'];

```
2. Define the number of allowed guesses (lives) for the player: You can define the number of allowed incorrect guesses the player can make before they lose the game. This can be adjusted based on the desired difficulty level of the game.
```js
let maxLives = 6;

```
## 2 - Select a word
1. Select a random word from the array of words: You can use the `Math.random()` function to generate a random index in the `words` array, and select the word at that index.
```js
let selectedWord = words[Math.floor(Math.random() * words.length)];

```
2. Create an array to represent the current state of the word: You can create an array with the same length as the selected word, with each letter replaced by a blank _.
```js
let currentWordState = Array(selectedWord.length).fill('_');
```
## 3 - Render the game UI
1. Create a container element for the game: You can create a container element in your HTML file to hold the game elements.
```html
<div id="hangman-game">
  <!-- Game elements will be added here -->
</div>
```
2. Display the current state of the word: You can display the current state of the word in the game container element, using the current state array created in step 2.
```js
let gameContainer = document.getElementById('hangman-game');
let wordDisplay = document.createElement('div');
wordDisplay.classList.add('word-display');
wordDisplay.innerText = currentWordState.join(' ');
gameContainer.appendChild(wordDisplay);

```
3. Display the number of remaining lives: You can display the number of remaining lives in the game container element, using the `maxLives` variable defined in step 1.
```js
let livesDisplay = document.createElement('div');
livesDisplay.classList.add('lives-display');
livesDisplay.innerText = `Lives: ${maxLives}`;
gameContainer.appendChild(livesDisplay);

```
4. Add an input field for the player to enter a letter: You can add an input field for the player to enter a letter in the game container element.
```js
let letterInput = document.createElement('input');
letterInput.setAttribute('type', 'text');
letterInput.setAttribute('maxlength', '1');
letterInput.addEventListener('input', handleLetterInput);
gameContainer.appendChild(letterInput);

```
### 3.1 Supporting images for hangman

```js
let lives = maxLives;
let hangmanImage = document.createElement('img');
hangmanImage.setAttribute('src', `hangman-${lives}.png`);
gameContainer.appendChild(hangmanImage);
```
In this example, we're using an `img` element to display an image of the hangman. We're starting with `maxLives` number of lives, and using that to determine which image to display `(hangman-6.png, hangman-5.png, etc.)`. You'll need to create the images yourself and save them with the appropriate filenames (hangman-6.png, hangman-5.png, etc.).

In your `handleLetterInput` function, you can update the `lives` variable and change the `src` attribute of the `hangmanImage` element to reflect the new number of `lives`. For example:

```js
function handleLetterInput() {
  let guessedLetter = letterInput.value;
  // Check if guessedLetter is in selectedWord and update currentWordState
  // ...

  if (!selectedWord.includes(guessedLetter)) {
    lives--;
    livesDisplay.innerText = `Lives: ${lives}`;
    hangmanImage.setAttribute('src', `hangman-${lives}.png`);
  }
}
```
In this example, we're decrementing `lives` and updating the `src` attribute of `hangmanImage` whenever the player makes an incorrect guess. You'll need to define what happens when the player runs out of lives and the hangman is fully drawn (e.g. displaying a message and disabling the input field).

## 4 - Handle player input

1. Add an event listener to the `input` field to listen for when the player enters a letter: You can use the `addEventListener()` method to listen for the `input` event on the `input` field.
```js
letterInput.addEventListener('input', handleLetterInput);

```
2. When a letter is entered, check if it matches any letters in the selected word: You can use the `includes()` method to check if the guessed letter is in the selected word.
```js
function handleLetterInput() {
  let guessedLetter = letterInput.value;
  if (selectedWord.includes(guessedLetter)) {
    // Letter is in the selected word
  } else {
    // Letter is not in the selected word
  }
}
```
3. If the letter matches, reveal the corresponding letter in the current state of the word: You can use a loop to check each letter in the selected word, and update the current state array to reveal any matching letters.
```js
function handleLetterInput() {
  let guessedLetter = letterInput.value;
  if (selectedWord.includes(guessedLetter)) {
    for (let i = 0; i < selectedWord.length; i++) {
      if (selectedWord[i] === guessedLetter) {
        currentWordState[i] = guessedLetter;
      }
    }
    wordDisplay.innerText = currentWordState.join(' ');
  } else {
    // Letter is not in the selected word
  }
}
```
4. If the letter does not match, decrement the number of remaining lives: You can decrement the `lives` variable and update the `livesDisplay` element to reflect the new number of lives.
```js
function handleLetterInput() {
  let guessedLetter = letterInput.value;
  if (selectedWord.includes(guessedLetter)) {
    // Letter is in the selected word
  } else {
    lives--;
    livesDisplay.innerText = `Lives: ${lives}`;
    // Update the hangman image here if you're using one
  }
}

```
## 5 - Check for game over
1. Check if the player has guessed all the letters in the selected word: You can use the `every()` method to check if every letter in the current state array is not a blank `_`.
```js
function handleLetterInput() {
  // ...
  if (currentWordState.every(letter => letter !== '_')) {
    // Player has won
  } else {
    // Player has not won yet
  }
}
```
2. If the player has guessed all the letters, display a message indicating that they have won: You can display a message in the game container element to indicate that the player has won.
3. If the player has run out of lives, display a message indicating that they have lost: You can display a message in the game container element to indicate that the player has lost.
```js
function handleLetterInput() {
  // ...
  if (lives === 0) {
    let message = document.createElement('div');
    message.innerText = `Sorry, you lost. The word was "${selectedWord}".`;
//...
  }
}
```
## 6 - Restart the game
1. Add a restart button to the game UI: You can create a button element in the game container element to allow the player to restart the game.
2. When the restart button is clicked, select a new word and reset the game state: You can define a `restartGame()` function that resets the game state, selects a new word, and updates the UI to reflect the new game state.
```js
function restartGame() {
  // Select a new word and create a new currentWordState array
  // ...
  // Update the UI with the new game state
  lives = maxLives;
  livesDisplay.innerText = `Lives: ${lives}`;
  // Update the hangman image here if you're using one
}

```

