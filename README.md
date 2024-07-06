# Simon Game

## Overview

The Simon Game is a simple web-based implementation of the classic memory game where players must repeat a sequence of button presses that gets progressively longer. This project is built using HTML, CSS, and JavaScript. The game includes sound effects, animations, and responsive design for a seamless experience on both desktop and mobile devices.

[Play the Simon Game](https://arbaazyaseen15.github.io/Simon-Game/)

## Project Structure

```
Simon-Game/
├── index.html
├── styles.css
├── index.js
├── sounds/
│   ├── blue.mp3
│   ├── green.mp3
│   ├── red.mp3
│   └── yellow.mp3
└── images/
    ├── home.png
    ├── my_account_edit.png
    ├── topics.png
    ├── posts.png
    └── class Diagram.png
```

### HTML

The HTML file defines the structure of the Simon Game. It includes the title, buttons for the game, and the level display. The buttons are color-coded to match the classic Simon game: red, blue, green, and yellow.

### CSS

The CSS file styles the game elements, providing a visually appealing interface. It also includes media queries to ensure the game is responsive and works well on mobile devices.

```css
body {
  text-align: center;
  background-color: #011F3F;
}

#level-title {
  font-family: 'Press Start 2P', cursive;
  font-size: 3rem;
  color: #FEF2BF;
}
#level-title-m {
  display: none;
}

.container {
  display: block;
  width: 50%;
  margin: auto;
}

.mbtn {
  display: none;
}

.btn {
  margin: 25px;
  display: inline-block;
  height: 180px;
  width: 180px;
  border: 10px solid black;
  border-radius: 20%;
}

.game-over {
  background-color: red;
  opacity: 0.8;
}

.red {
  background-color: red;
}

.green {
  background-color: green;
}

.blue {
  background-color: blue;
}

.yellow {
  background-color: yellow;
}

.pressed {
  box-shadow: 0 0 20px white;
  background-color: grey;
}

@media (max-width: 800px) {
  #level-title {
    display: none;
  }
  #level-title-m {
    display: block;
    font-family: 'Press Start 2P', cursive;
    font-size: 3rem;
    color: #FEF2BF;
  }
  .container {
    display: block;
    width: 100%;
    margin: auto;
  }
  .btn {
    margin: 15px;
    display: inline-block;
    height: 90px;
    width: 90px;
    border: 5px solid black;
    border-radius: 20%;
  }
  .mbtn {
    display: inline-block;
    font-weight: 100;
    font-family: monospace;
    font-size: 1.4rem;
    color: white;
    padding: 1rem 3rem;
    text-decoration: none;
    box-shadow: inset 0 0 2px white,
                1px 1px 2px white,
                -1px -1px 1px white;
    border-radius: 5px;
    background-color: black;
    border: none;
    margin-top: 20px;
  }
  .mbtn:hover {
    opacity: .7;
    transform: scale(.95);
    transition: all .2s ease;
  }
}
```

### JavaScript

The JavaScript file implements the game logic. It handles user interactions, game sequence generation, checking user input, playing sounds, and animating button presses.

```javascript
var userClickedPattern = [];
var buttonColors = ["red", "blue", "green", "yellow"];
var gamePattern = [];
var randomChosenColor;
var level = 0;
var lastAnswer = 0;

function nextSequence() {
    level += 1;
    $("#level-title, #level-title-m").text("Level " + level);
    var randomNumber = Math.floor(Math.random() * 4);
    randomChosenColor = buttonColors[randomNumber];
    gamePattern.push(randomChosenColor);
    $('#' + randomChosenColor).fadeOut().fadeIn('slow');
    playSound(randomChosenColor);
}

$(".btn").on("click", function () {
    var userChosenColor = $(this).attr('id');
    userClickedPattern.push(userChosenColor);
    playSound(userChosenColor);
    animatePress(userChosenColor);
    checkAnswer(lastAnswer);
});

function playSound(name) {
    var audio = new Audio(name + '.mp3');
    audio.play();
}

function animatePress(currentColor) {
    $('.' + currentColor).addClass("pressed");
    setTimeout(function () {
        $('.' + currentColor).removeClass("pressed");
    }, 100);
}

if ($(window).width() < 800) {
    $(".mbtn").on("click", function () {
        $(this).hide();
        nextSequence();
        $(".mbtn").off("click");
    });
} else {
    $(document).on("keypress", function () {
        nextSequence();
        $(document).off("keypress");
    });
}

function checkAnswer(currentLevel) {
    if (userClickedPattern[currentLevel] == gamePattern[currentLevel]) {
        if (lastAnswer == (level - 1)) {
            setTimeout(nextSequence(), 1000);
            lastAnswer = 0;
            userClickedPattern = [];
        } else {
            lastAnswer += 1;
            return;
        }
    } else {
        $("#level-title,  #level-title-m").text("Wrong Answer!!!");
        alert("Congratulations, You Have Reached " + level + " level");
        setTimeout(function () {
            $("#level-title").text("Press A key to start again");
        }, 3000);
        $(".mbtn").show();
        $(".mbtn").text("Restart");
        $(".mbtn").on("click", function () {
            $(this).hide();
            nextSequence();
            $(".mbtn").off("click");
        });
        restart();
    }
}

function restart() {
    level = 0;
    gamePattern = [];
    userClickedPattern = [];
    lastAnswer = 0;
    return;
}
```

## Features

- **Responsive Design:** The game adjusts to different screen sizes, ensuring a great user experience on both desktop and mobile devices.
- **Sound Effects:** Each button press is accompanied by a sound effect to enhance the gameplay experience.
- **Visual Feedback:** Button presses are visually indicated with animations.
- **Game Levels:** The game progresses in levels, increasing in difficulty as the user successfully completes each sequence.

## How to Play

1. **Start the Game:** Press any key (on desktop) or tap the start button (on mobile) to begin.
2. **Repeat the Sequence:** Watch the sequence of button flashes and repeat it by clicking the buttons in the correct order.
3. **Progress Through Levels:** Successfully repeat the sequence to move to the next level. The sequence will get longer with each level.
4. **Game Over:** If you click the wrong button, the game will alert you and display your progress. You can restart the game by pressing any key or tapping the restart button.

## Conclusion

The Simon Game project is a fun and interactive way to test and improve your memory skills. By utilizing HTML, CSS, and JavaScript, the game provides a responsive and engaging experience for users of all ages. Whether you're playing on a desktop or mobile device, the Simon Game challenges you to remember and repeat increasingly complex sequences of colors and sounds.

[Play the Simon Game](https://arbaazyaseen15.github.io/Simon-Game/)
