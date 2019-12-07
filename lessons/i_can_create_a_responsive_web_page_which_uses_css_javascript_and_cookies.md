# I Can Create a Responsive Web Page Which Uses CSS, JavaScript, and Cookies




## Web Page Source Code

### Rock, Paper, Scissors

```
<html>
<head>
    <script>
        //
        var ROCK = 0;
        var PAPER = 1;
        var SCISSORS = 2;
        //
        var myScore = 0;
        var computerScore = 0;
        function getRandomWholeNumberUnder(range) {
            return Math.floor(Math.random()*range);
        }
        function updateIcon(target, selection) {
            var imgSrc = "https://img.icons8.com/plasticine/100/000000/question-mark.png";
            if (selection == ROCK) {
                imgSrc = "https://img.icons8.com/color/48/000000/rock.png";
            } else if (selection == PAPER) {
                imgSrc = "https://img.icons8.com/dusk/64/000000/paper.png";
            } else if (selection == SCISSORS) {
                imgSrc = "https://img.icons8.com/plasticine/100/000000/scissors.png";
            }
            document.getElementById(target).src = imgSrc;
        }
        function playRockPaperScissors(mySelection) {
            var computerSelection = getRandomWholeNumberUnder(3);
            var outcome;
            if (mySelection == ROCK) {
                if (computerSelection == ROCK) {
                    outcome = "It's a tie, try again:";
                } else if (computerSelection == PAPER) {
                    outcome = "You lose, try again:";
                    computerScore = computerScore + 1;
                } else if (computerSelection == SCISSORS) {
                    outcome = "You win, try again:";
                    myScore = myScore + 1;
                }
            } else if (mySelection == PAPER) {
                if (computerSelection == ROCK) {
                    outcome = "You win, try again:";
                    myScore = myScore + 1;
                } else if (computerSelection == PAPER) {
                    outcome = "It's a tie, try again:";
                } else if (computerSelection == SCISSORS) {
                    outcome = "You lose, try again:";
                    computerScore = computerScore + 1;
                }
            } else if (mySelection == SCISSORS) {
                if (computerSelection == ROCK) {
                    outcome = "You lose, try again:";
                    computerScore = computerScore + 1;
                } else if (computerSelection == PAPER) {
                    outcome = "You win, try again:";
                    myScore = myScore + 1;
                } else if (computerSelection == SCISSORS) {
                    outcome = "It's a tie, try again:";
                }
            }
            updateDisplay(mySelection, computerSelection, outcome);
        }
        function updateDisplay(mySelection, computerSelection, outcome) {
            //show my icon
            updateIcon("my_selection", mySelection);
            //show computer icon
            updateIcon("computer_selection", computerSelection);
            //show outcome
            document.getElementById("result").innerHTML = outcome;
            //update my score
            document.getElementById("my_score").innerHTML = myScore;
            //update computer score
            document.getElementById("computer_score").innerHTML = computerScore;
        }
    </script>
    <style>
        div.wrapper {
            width: 400px;
            margin-left: auto;
            margin-right: auto;
            border: 1px black solid;
        }
        div.title {
            text-align: center;
        }
        div.computer {
            width: 130px;
            display: inline-block;
        }
        div.game {
            width: 130px;
            display: inline-block;
        }
        div.selected_icon {
            width: 50px;
            text-align: center;
            display: inline-block;
        }
        div.me {
            width: 130px;
            display: inline-block;
        }
        div.selection {
            text-align: center;
        }
        div.selection_icon {
            width: 100px;
            text-align: center;
            display: inline-block;
        }
        img.selection_icon {
            text-align: center;
            width: 32px;
            height: 32px;
            display: inline-block;
        }
        span.title {
            font-size: 36pt;
        }
    </style>
</head>
<body>
    <div class="wrapper">
        <div class="title">
            <span class="title">Rock Paper Scissors</span>
        </div>
        <div class="computer">
            <p>Computer Score:</p>
            <p id="computer_score"></p>
        </div>
        <div class="game">
            <div class="selected_icon">
                <img class="selection_icon" id="computer_selection"/>
            </div>
            <div class="selected_icon">
                <img class="selection_icon" id="my_selection"/>
            </div>
        </div>
        <div class="me">
            <p>My Score:</p>
            <p id="my_score"></p>
        </div>
        <div class="selection">
            <p id="result"></p>
            <div>
                <div class="selection_icon">
                    <img class="selection_icon"
                         src="https://img.icons8.com/color/48/000000/rock.png"
                        onclick="playRockPaperScissors(ROCK)"/>
                </div>
                <div class="selection_icon">
                    <img class="selection_icon"
                         src="https://img.icons8.com/dusk/64/000000/paper.png"
                        onclick="playRockPaperScissors(PAPER)"/>
                </div>
                <div class="selection_icon">
                    <img class="selection_icon"
                         src="https://img.icons8.com/plasticine/100/000000/scissors.png"
                        onclick="playRockPaperScissors(SCISSORS)"/>
                </div>
            </div>
        </div>
    </div>
    <script>
        updateDisplay(null, null, "Make a selection by clicking an icon:");
    </script>
</body>
</html>
```