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

Example functions: 
```js
checkForWinner();
checkForTie();
switchPlayers();
```

6. Switch players: Write a function to switch players after each move. You can use an if statement to toggle between X and O.

## 4 - Create game logic
## 5 - Handle player input
## 6 - Update the game state
## 7 - Display the winner or tie message
## 8 - Allow players to restart
