Hi Meta you and I built this cool game together I'm about to commit it to GITHUB and I'd like you to contribute to the README to describe what the code in script.js does and how we got there together.

Thanks again for your collaboration...

const startButton = document.getElementById('start');
let doorImage1 = document.getElementById('door1');
let doorImage2 = document.getElementById('door2');
let doorImage3 = document.getElementById('door3');

let botDoorPath = "images/monkey-door.svg";
let beachDoorPath = "images/sex-door.svg";
let spaceDoorPath = "images/drugs-door.svg";
let closedDoorPath = "images/closed_door.svg";

let numClosedDoors = 3;
let openDoor1;
let openDoor2;
let openDoor3;
let currentlyPlaying = true;
let clickedDoors = [];

const startRound = () => {
  console.log("Start Round initiated");
  clickedDoors = [];
  doorImage1.src = closedDoorPath;
  doorImage2.src = closedDoorPath;
  doorImage3.src = closedDoorPath;
  numClosedDoors = 3;
  currentlyPlaying = true;
  startButton.innerHTML = 'Good Luck';
  randomChoreDoorGenerator();
}

const isClicked = (door) => {
  console.log(`Checking if door ${door.id} is clicked`);
  return clickedDoors.includes(door.id);
}

const isBot = (door) => {
  const doorPath = door.src.split('/').pop(); // Extract filename
  console.log(`Comparing ${doorPath} with ${botDoorPath}`);
  if (doorPath === botDoorPath.split('/').pop()) {
    console.log(`Door ${door.id} has bot`);
    return true;
  } else {
    console.log(`Door ${door.id} does not have bot`);
    return false;
  }
}

const playDoor = (door) => {
  console.log(`Playing door ${door.id}`);
  if (isBot(door)) {
    console.log('Bot door found!');
    gameOver('lose');
  } 
  numClosedDoors--;
  console.log(`Remaining closed doors: ${numClosedDoors}`);
  if (numClosedDoors === 0) {
    gameOver('win');
  }
}

const randomChoreDoorGenerator = () => {
  console.log("Generating random chore door");
  const choreDoor = Math.floor(Math.random() * numClosedDoors);
  console.log(`Chore door number: ${choreDoor}`);
  if (choreDoor === 0) {
    openDoor1 = botDoorPath;
    openDoor2 = beachDoorPath;
    openDoor3 = spaceDoorPath;
  } else if (choreDoor === 1) {
    openDoor2 = botDoorPath;
    openDoor1 = beachDoorPath;
    openDoor3 = spaceDoorPath;
  } else {
    openDoor3 = botDoorPath;
    openDoor1 = beachDoorPath;
    openDoor2 = spaceDoorPath;
  }
  console.log(`Open door paths: ${openDoor1}, ${openDoor2}, ${openDoor3}`);
}

doorImage1.onclick = () => {
  console.log(`Door 1 clicked`);
  if (currentlyPlaying && !isClicked(doorImage1)) {
    doorImage1.src = openDoor1;
    clickedDoors.push(doorImage1.id);
    playDoor(doorImage1);
  }
}

doorImage2.onclick = () => {
  console.log(`Door 2 clicked`);
  if (currentlyPlaying && !isClicked(doorImage2)) {
    doorImage2.src = openDoor2;
    clickedDoors.push(doorImage2.id);
    playDoor(doorImage2);
  }
}

doorImage3.onclick = () => {
  console.log(`Door 3 clicked`);
  if (currentlyPlaying && !isClicked(doorImage3)) {
    doorImage3.src = openDoor3;
    clickedDoors.push(doorImage3.id);
    playDoor(doorImage3);
  }
}

let gameStatus = '';

const gameOver = (status) => {
  console.log(`Game over with status: ${status}`);
  gameStatus = status;
  if (status === 'win') {
    startButton.innerHTML = 'You win! Play again?';
  } else {
    startButton.innerHTML = 'Game over! Play again?';
  }
  currentlyPlaying = false;
}

startButton.addEventListener('click', () => {
  if (!currentlyPlaying) {
    if (gameStatus === 'lose') {
      customAlert();
    }
    startRound();
  }
});

function customAlert() {
  document.getElementById('custom-alert').style.display = 'block';
  document.getElementById('alert-title').innerHTML = title;
  document.getElementById('alert-message').innerHTML = message;
}

function closeCustomAlert() {
  document.getElementById('custom-alert').style.display = 'none';
}

document.addEventListener('DOMContentLoaded', () => {
  console.log("Document loaded, starting round");
  startRound();
});

Game Description
This is a simple door-opening game where the player must avoid opening the door with the "bot" behind it. The game features three doors, one of which is randomly assigned the "bot" door.
How to Play
Click the "Start" button to begin a new round.
Click on one of the three doors to open it.
If the door has the "bot" behind it, the game ends and the player loses.
If all doors are opened without finding the "bot," the player wins.
Script.js Explanation
The script.js file contains the game logic, which is divided into several functions:
Game Initialization
startRound(): Resets the game state, closes all doors, and generates a new random "bot" door.
Door Interaction
isClicked(door): Checks if a door has already been clicked.
isBot(door): Checks if a door has the "bot" behind it.
playDoor(door): Handles door opening logic, checking for the "bot" and updating game state.
Game Over
gameOver(status): Ends the game, updates the start button text, and displays an alert if the player loses.
Event Listeners
Door clicks: Open the corresponding door and play the door logic.
Start button clicks: Restart the game if it's not currently playing.
Custom Alert
customAlert(): Displays a custom alert box when the player loses.
DOM Content Loaded
Initializes the game by calling startRound().
Collaboration
This game was developed in collaboration with Frederick Viedge and Meta AI.
