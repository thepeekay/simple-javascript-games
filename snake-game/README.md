**1. Define the game data:**
* Define the size of the game board.
* Define the starting position and length of the snake.
* Define the starting position and movement direction of the food.
* Define the initial game speed and the rate of increase in speed.

**2. Render the game UI:**
* Create a container element for the game.
* Draw the game board, snake, and food on the container element.
* Display the current score.

**3. Handle player input:** 
* Add an event listener to the document to listen for when the player presses arrow keys.
* When an arrow key is pressed, update the snake's movement direction.

**4. Update the game state:** 
* Update the snake's position based on its movement direction.
* Check if the snake has collided with the game board or itself.
* If the snake has collided, end the game.
* If the snake has eaten the food, update the score and generate a new food.
* Increase the game speed over time.

**5. Render the updated game state:**
* Update the UI to display the updated snake, food, and score.

**6. Restart the game:**
* Add a restart button to the game UI.
* When the restart button is clicked, reset the game state and update the UI.

## 1 - Define the game data
1. Define the size of the game board: You can define the width and height of the game board in number of cells. The game board can be a grid of cells, where each cell can have a size and color. 
```js 
let boardWidth = 20;
let boardHeight = 20;
```
2. Define the starting position and length of the snake: You can define the starting position and length of the snake as an array of cells. Each cell can have an `x` and `y` coordinate, representing its position on the game board.
```js 
let snake = [
  { x: 5, y: 5 },
  { x: 4, y: 5 },
  { x: 3, y: 5 },
];
let snakeLength = 3;
```
3. Define the starting position and movement direction of the food: You can define the starting position of the food as a cell with a random `x` and `y` coordinate, and the movement direction as an object with `x` and `y` components.
```js
let food = {
  x: Math.floor(Math.random() * boardWidth),
  y: Math.floor(Math.random() * boardHeight),
};
let foodDirection = { x: 1, y: 0 };

```
4. Define the initial game speed and the rate of increase in speed: You can define the initial speed of the game in milliseconds per frame, and the rate of increase in speed in milliseconds per second.
```js
let gameSpeed = 100;
let speedIncrease = 10;

```
## 2 - Render the game UI
### 2.1 Using `Canvas` element
1. Create a container element for the game: You can create a container element in your HTML file to hold the game elements. 
```html 
<div id="snake-game">
  <!-- Game elements will be added here -->
</div>

```
2. Draw the game board, snake, and food on the container element: You can create a canvas element in the game container element to draw the game board, snake, and food. You can define the size and color of the cells and the snake, and the color and size of the food.
```js
let canvas = document.createElement('canvas');
canvas.width = boardWidth * cellSize;
canvas.height = boardHeight * cellSize;
gameContainer.appendChild(canvas);

let ctx = canvas.getContext('2d');

// Draw the game board
ctx.fillStyle = '#333';
ctx.fillRect(0, 0, canvas.width, canvas.height);

// Draw the snake
ctx.fillStyle = '#fff';
snake.forEach(cell => {
  ctx.fillRect(cell.x * cellSize, cell.y * cellSize, cellSize, cellSize);
});

// Draw the food
ctx.fillStyle = '#f00';
ctx.fillRect(food.x * cellSize, food.y * cellSize, cellSize, cellSize);

```
3. Display the current score: You can display the current score in the game container element, using a separate element or a part of the canvas.
```js
let scoreDisplay = document.createElement('div');
scoreDisplay.innerText = `Score: ${score}`;
gameContainer.appendChild(scoreDisplay);

```
### 2.2 Using just HTML elements

Canvas might be challenging so here is a suggestion with just HTML elements.
1. In this example, we're using four separate HTML elements to represent the game board, snake, food, and score. The game board is represented as a grid of cells inside a `div` element with the class `game-board`. 

```html
<div id="snake-game">
  <div class="game-board">
    <!-- Game board cells will be added here -->
  </div>
  <div class="snake"></div>
  <div class="food"></div>
  <div class="score">Score: 0</div>
</div>

```
You can use CSS to style the cells as needed:
```css
.game-board {
  display: grid;
  grid-template-columns: repeat(20, 1fr);
  grid-template-rows: repeat(20, 1fr);
  width: 400px;
  height: 400px;
  border: 1px solid #333;
}

.game-board > div {
  border: 1px solid #333;
  background-color: #111;
}

```
2. The snake is represented as a `div` element with the class `snake`, and its position and length are controlled with JavaScript:
```css
.snake {
  position: absolute;
  width: 20px;
  height: 20px;
  background-color: #fff;
}

```
The food is also represented as a `div` element with the class `food`, and its position is controlled with JavaScript:

```css
.food {
  position: absolute;
  width: 20px;
  height: 20px;
  background-color: #f00;
}

```
The score is represented as a `div` element with the class `score`, and its value is updated with JavaScript:

```css
.score {
  margin-top: 10px;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
}

```

## 3 - Handle player input
1. Add an event listener to the document to listen for when the player presses arrow keys: You can use the `addEventListener()` method to listen for the `keydown` event on the document. You can update the snake's movement direction based on which arrow key is pressed.
```js
document.addEventListener('keydown', handleKeyDown);

function handleKeyDown(event) {
  switch (event.key) {
    case 'ArrowUp':
      snakeDirection = { x: 0, y: -1 };
      break;
    case 'ArrowDown':
      snakeDirection = { x: 0, y: 1 };
      break;
    case 'ArrowLeft':
      snakeDirection = { x: -1, y: 0 };
      break;
    case 'ArrowRight':
      snakeDirection = { x: 1, y: 0 };
      break;
  }
}

```
2. When an arrow key is pressed, update the snake's movement direction: You can define a `snakeDirection` variable to store the current movement direction of the snake. When an arrow key is pressed, you can update this variable based on the key pressed.
```js
let snakeDirection = { x: 1, y: 0 };

function handleKeyDown(event) {
  switch (event.key) {
    case 'ArrowUp':
      snakeDirection = { x: 0, y: -1 };
      break;
    case 'ArrowDown':
      snakeDirection = { x: 0, y: 1 };
      break;
    case 'ArrowLeft':
      snakeDirection = { x: -1, y: 0 };
      break;
    case 'ArrowRight':
      snakeDirection = { x: 1, y: 0 };
      break;
  }
}

```
## 4 - Update the game state
1. Update the snake's position based on its movement direction: You can update the snake's position based on its movement direction. You can do this by adding a new cell to the front of the snake and removing the last cell, effectively moving the snake in its current direction.
```js
function updateSnake() {
  // Add a new head cell to the front of the snake
  let newHead = {
    x: snake[0].x + snakeDirection.x,
    y: snake[0].y + snakeDirection.y,
  };
  snake.unshift(newHead);

  // Remove the last cell of the snake
  if (snake.length > snakeLength) {
    snake.pop();
  }
}
```
2. Check if the snake has collided with the game board or itself: You can check if the snake's head has collided with the game board or any part of its body. If it has, the game is over.
```js
function checkCollisions() {
  // Check if the snake's head has collided with the game board or itself
  let head = snake[0];
  if (
    head.x < 0 ||
    head.y < 0 ||
    head.x >= boardWidth ||
    head.y >= boardHeight ||
    snake.slice(1).some(cell => cell.x === head.x && cell.y === head.y)
  ) {
    gameOver();
  }
}

```
Let's explain in more detail, as `checkCollisions()` and `updateSnake()` functions can be a little daunting.

The `updateSnake()` function is responsible for updating the position of the snake based on its current movement direction. Here's how it works:

* First, we create a new `newHead` object that represents the next position of the snake's head. We calculate its `x` and `y` coordinates by adding the `x` and `y` components of the `snakeDirection` vector to the `x` and `y` coordinates of the current head cell of the snake.
* Next, we add the new head cell to the front of the snake array using the `unshift()` method. This effectively moves the snake in its current direction.
* Finally, we remove the last cell of the snake using the `pop()` method, but only if the `length` of the snake is greater than the `snakeLength` variable. This ensures that the snake doesn't grow indefinitely.

`pop()` and `unshift()` are array functions

The `checkCollisions()` function is responsible for checking if the snake has collided with the game board or itself. Here's how it works:

* First, we get the head cell of the snake by accessing the first element of the `snake` array.
Then, we check if the `x` or `y` coordinates of the head cell are outside the bounds of the game board. If they are, we know that the snake has collided with the game board.
* Next, we use the `slice()` method to create a new array containing all the cells of the snake except for the head cell. We use the `some()` method to check if any of these cells have the same `x` and `y` coordinates as the head cell. If they do, we know that the snake has collided with itself.
* Finally, if the snake has collided with the game board or itself, we call the `gameOver()` function to end the game.

3. If the snake has collided, end the game: You can define a `gameOver()` function that stops the game loop, displays a message to the player, and allows them to restart the game.
```js
function gameOver() {
  // Reset text and score
  // Reset interval
  // Show a restart button etc. etc.
}

```
4. If the snake has eaten the food, update the score and generate a new food: You can check if the snake's head has collided with the food. If it has, you can update the score, generate a new food at a random position, and increase the snake's length.
```js
function checkFood() {
  // Check if the snake's head has collided with the food
  let head = snake[0];
  if (head.x === food.x && head.y === food.y) {
    // Update the score
    score++;
    scoreDisplay.innerText = `Score: ${score}`;

    // Generate a new food
    food = {
      x: Math.floor(Math.random() * boardWidth),
      y: Math.floor(Math.random() * boardHeight),
    };

    // Increase the snake's length
    snakeLength++;
  }
}

```
5. Increase the game speed over time: You can increase the game speed over time by reducing the time interval between each game loop iteration. You can define a `speedUp()` function that reduces the `gameSpeed` variable by a certain amount, and call it at a regular interval using the `setInterval()` method.
## 5 - Render the updated game state

1. Update the snake's position on the game board: You can update the position of the snake on the game board by updating the HTML elements that represent the snake. You can use the `style` property to set the position of the `div` element that represents each cell of the snake.
```js
function renderSnake() {
  snake.forEach((cell, index) => {
    let snakeCell = document.createElement('div');
    snakeCell.classList.add('snake-cell');
    snakeCell.style.gridRowStart = cell.y + 1;
    snakeCell.style.gridColumnStart = cell.x + 1;
    snakeElement.appendChild(snakeCell);
  });
}

```
2. Update the position of the food on the game board: You can update the position of the food on the game board by updating the HTML element that represents the food. You can use the `style` property to set the position of the `div` element that represents the food.
```js
function renderFood() {
  let foodElement = document.createElement('div');
  foodElement.classList.add('food');
  foodElement.style.gridRowStart = food.y + 1;
  foodElement.style.gridColumnStart = food.x + 1;
  gameBoard.appendChild(foodElement);
}

```
3. Update the score display: You can update the score display by updating the text content of the HTML element that represents the score.
```js
function updateScore() {
  scoreDisplay.textContent = `Score: ${score}`;
}

```
4. Remove any old snake cells or food elements: You can remove any old snake cells or food elements from the game board by using the `querySelectorAll()` method to select all elements with the class `snake-cell` or `food`, and then removing them with the `remove()` method.
```js
function clearBoard() {
  let oldSnakeCells = document.querySelectorAll('.snake-cell');
  oldSnakeCells.forEach(cell => cell.remove());

  let oldFood = document.querySelector('.food');
  if (oldFood) {
    oldFood.remove();
  }
}

```

## 6 - Restart the game
1. Restarting the game
```js
function restartGame() {
  // Reset game state variables
  score = 0;
  snakeLength = 3;
  snakeDirection = { x: 1, y: 0 };
  snake = [
    { x: 2, y: 0 },
    { x: 1, y: 0 },
    { x: 0, y: 0 },
  ];
  food = {
    x: Math.floor(Math.random() * boardWidth),
    y: Math.floor(Math.random() * boardHeight),
  };

  // Clear game board and update score display
  // ..

  // Restart game loop
  // ..

  // Remove restart button and game over message
  let restartButton = document.querySelector('button');
  restartButton.remove();
  let gameOverMessage = document.querySelector('div');
  gameOverMessage.remove();
}
```
The `restartGame()` function is responsible for resetting the game state variables to their initial values, clearing the game board, and restarting the game loop. Here's how it works:

* First, we reset the `score`, `snakeLength`, `snakeDirection`, `snake`, and `food` variables to their initial values.
* Then, we clear the game board and update the score display using the `clearBoard()` and `updateScore()` functions.
* Next, we stop the current game loop using the `clearInterval()` method, and restart it using the `setInterval()` method.
* Finally, we remove the restart button and game over message elements from the game container using the `remove()` method.
