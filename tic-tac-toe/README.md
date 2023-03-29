# Tic tac toe in JS
Simple tic tac toe game in JS 

1. **Create the HTML structure:** Create a simple HTML structure that includes the game board, the cells, and any other necessary elements.

2. **Style the game board:** Use CSS to style the game board and cells to make it visually appealing.

3. **Initialize the game:** Use JavaScript to initialize the game by creating an empty game board, determining who goes first, and displaying a message to indicate whose turn it is.

4. **Create game logic:** Write JavaScript functions to handle game logic, including determining a winner, checking for a tie, and updating the game board.

5. **Handle player input:** Add event listeners to the cells on the game board so that players can select a cell and make a move.

6. **Update the game state:** When a player makes a move, update the game state by updating the game board, checking for a winner or tie, and switching to the next player's turn.

7. **Display the winner or tie message:** When the game ends, display a message indicating who won or if the game ended in a tie.

8. **Allow players to restart:** Add a button or link that allows players to restart the game, resetting the game board and starting over.

## 1 - Create the HTML structure

1. Create an HTML file: Start by creating a new HTML file and opening it in a code editor of your choice.

2. Create a container div: Create a container div that will hold the game board and any other elements you want to include in your game.

Example:
```html
<div id="container"></div>
```

3. Create the game board: Inside the container div, create a game board using an HTML table. The game board should have 3 rows and 3 columns, with each cell having an ID to help identify it later.

Example: 
```html
<table id="game-board">
  <tr>
    <td id="cell-0"></td>
    <td id="cell-1"></td>
    <td id="cell-2"></td>
  </tr>
  <tr>
    <td id="cell-3"></td>
    <td id="cell-4"></td>
    <td id="cell-5"></td>
  </tr>
  <tr>
    <td id="cell-6"></td>
    <td id="cell-7"></td>
    <td id="cell-8"></td>
  </tr>
</table>
```

4. Add any other necessary elements: You can add any other elements you want, such as a message area to display whose turn it is, a scoreboard, or a button to restart the game.

5. Link your HTML file to a JavaScript file: Finally, link your HTML file to a JavaScript file that will contain the game logic and event handlers.

## 2 - Style the game board

1. Create a CSS file: Start by creating a new CSS file in your code editor of choice. You can name it `styles.css` or any other name you prefer.

Example:
```css
#container {
  width: 400px;
  height: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
```

2. Style the container: In your CSS file, begin by styling the container div to set its width and height, and to center the game board on the page.
Example:
```css
#game-board {
  border-collapse: collapse;
}

td {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  text-align: center;
  vertical-align: middle;
  font-size: 48px;
  font-weight: bold;
  background-color: white;
}
```

3. Style the game board: Next, style the game board by setting the width and height of each cell, as well as the background color, font size, and alignment of the text inside each cell.

4. Style the active and winner cells: Add styles to highlight the active cell (the cell where the current player can make a move) and the winner cells (the cells that form a winning combination).

5. Style the message and restart button: Finally, style any other elements you added, such as the message area and the restart button.

## 3 - Initialize the game
1. Create a JavaScript file: Start by creating a new JavaScript file in your code editor of choice. You can name it app.js or any other name you prefer.

2. Initialize the game board: In your JavaScript file, create an array to represent the game board. You can use null to represent empty cells, and X and O to represent player moves.

Example:
```js
let board = [
  null, null, null,
  null, null, null,
  null, null, null
];
```

3. Determine who goes first: Write a function to determine who goes first. You can use Math.random() to generate a random number between 0 and 1, and assign the first move to the player with the higher number.

Example:

```js
function determineFirstPlayer() {
  let player1 = Math.random();
  let player2 = Math.random();
  if (player1 > player2) {
    return 'X';
  } else {
    return 'O';
  }
}

let currentPlayer = determineFirstPlayer();

```
4. Display a message: Write a function to display a message indicating whose turn it is. You can use the currentPlayer variable to determine whose turn it is.

```js
function displayMessage(message) {
  let messageElement = document.getElementById('message');
  messageElement.innerText = message;
}

displayMessage(`Player ${currentPlayer}'s turn`);

```
5. Add event listeners: Write a function to add event listeners to the cells on the game board. You can use the addEventListener() method to listen for clicks on each cell, and update the game state when a player makes a move.

Example: 
```js
checkForWinner();
checkForTie();
switchPlayers();
```

```js
let cells = document.querySelectorAll('td');

function addEventListeners() {
  cells.forEach((cell, index) => {
    cell.addEventListener('click', () => {
      if (board[index] === null) {
        board[index] = currentPlayer;
        cell.innerText = currentPlayer;
        cell.classList.add('active');
        checkForWinner();
        checkForTie();
        switchPlayers();
      }
    });
  });
}

addEventListeners();

```

6. Switch players: Write a function to switch players after each move. You can use an if statement to toggle between X and O.
```js
function switchPlayers() {
  if (currentPlayer === 'X') {
    currentPlayer = 'O';
  } else {
    currentPlayer = 'X';
  }
  displayMessage(`Player ${currentPlayer}'s turn`);
}

```

## 4 - Create game logic

1. Write a function to check for a winner: In your JavaScript file, write a function to check if a player has won the game. You can define an array of winning combinations, and check if any of the combinations match the current game board.
Example: 
```js
function checkForWinner() {
  let winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];

  let winner = null;

  winningCombinations.forEach(combination => {
    let [a, b, c] = combination;
    if (board[a] !== null && board[a] === board[b] && board[b] === board[c]) {
      winner = board[a];
      highlightWinnerCells(combination);
    }
  });

  if (winner !== null) {
    displayMessage(`Player ${winner} wins!`);
    removeEventListeners();
  }
}
```

2. Write a function to check for a tie: Write a function to check if the game has ended in a tie. You can check if all the cells on the game board are filled with a player move, and if there is no winner.

Example:

```js
function checkForTie() {
  if (!board.includes(null)) {
    displayMessage('Tie game!');
    removeEventListeners();
  }
}
```

3. Write a function to update the game board: Write a function to update the game `board` when a player makes a move. You can update the `board` array and update the text of the cell that was clicked.

```js
function updateGameBoard(index) {
  board[index] = currentPlayer;
  let cell = cells[index];
  cell.innerText = currentPlayer;
  cell.classList.add('active');
}
```

4. Write a function to highlight winner cells: Write a function to highlight the cells that form a winning combination. You can add a CSS class to the cells that belong to the winning combination.

5. Write a function to remove event listeners: Write a function to remove the event listeners from the cells on the game board. This is necessary when the game ends, to prevent players from making additional moves.

## 5 - Handle player input

1. Add event listeners to cells: In your JavaScript file, write a function to add event listeners to the cells on the game board. You can use the addEventListener() method to listen for clicks on each cell, and update the game state when a player makes a move.

Example:
```js
function addEventListeners() {
  cells.forEach((cell, index) => {
    cell.addEventListener('click', () => {
      if (board[index] === null) {
        updateGameBoard(index);
        checkForWinner();
        checkForTie();
        switchPlayers();
      }
    });
  });
}

```

2. Remove event listeners: Write a function to remove the event listeners from the cells on the game board. This is necessary when the game ends, to prevent players from making additional moves.
Example: 
```js
function removeEventListeners() {
  cells.forEach(cell => {
    cell.removeEventListener('click', switchPlayers);
  });
}

```

3. Call addEventListeners(): Call the addEventListeners() function to add event listeners to the cells when the game is initialized.


## 6 - Update the game state

1. Update the game state: In your JavaScript file, write a function to update the game state after a player makes a move. You can update the `board` array, update the text of the cell that was clicked, and switch to the next player's turn.

```js
function updateGameState(index) {
  board[index] = currentPlayer;
  let cell = cells[index];
  cell.innerText = currentPlayer;
  cell.classList.add('active');
  switchPlayers();
}
```
2. Call updateGameState(): Update the addEventListeners() function to call the updateGameState() function when a player clicks on a cell.
```js
function addEventListeners() {
  cells.forEach((cell, index) => {
    cell.addEventListener('click', () => {
      if (board[index] === null) {
        updateGameState(index);
        checkForWinner();
        checkForTie();
      }
    });
  });
}
```

## 7 - Display the winner or tie message

1. Restart the game: In your JavaScript file, write a function to restart the game. You can reset the board array to its initial state, clear the text and styles of the cells, and initialize the game with a new first player.

```js
function restartGame() {
  board = [
    null, null, null,
    null, null, null,
    null, null, null
  ];
  cells.forEach(cell => {
    cell.innerText = '';
    cell.classList.remove('active', 'winner');
  });
  currentPlayer = determineFirstPlayer();
  displayMessage(`Player ${currentPlayer}'s turn`);
  addEventListeners();
}
```
2. Call restartGame(): Update the restart button in your HTML file to call the `restartGame()` function when it is clicked.
```js
<button id="restart" onclick="restartGame()">Restart Game</button>
```

## 8 - Allow players to restart

1. Create the game loop: In your JavaScript file, create a game loop that checks if the game has ended and takes appropriate action. You can use a `while` loop that runs as long as the game is not over, and checks for a winner or a tie after each move.

```js
let gameIsOver = false;

while (!gameIsOver) {
  // Player makes a move
  // Update the game state
  // Check for winner or tie
  // If there is a winner or tie, end the game
}

```
2. End the game: When the game ends, set `gameIsOver` to `true` and remove the event listeners from the cells on the game board.
```js
gameIsOver = true;
removeEventListeners();
```
3. Restart the game: After the game ends, you can ask the player if they want to play again, and restart the game if they do
