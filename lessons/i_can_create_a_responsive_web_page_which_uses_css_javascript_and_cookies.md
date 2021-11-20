# I Can Create a Responsive Web Page Which Uses CSS, JavaScript, and Cookies

## What's This About?

This lesson reviews how to use CSS, JavaScript, and Cookies to create
a very simple video game - Rock, Paper, Scissors - the source code of which
can be found at the bottom of this web page.

### What Is a Responsive Web Page?

Traditionally, web pages have only been loaded onto one type of device - a computer,
either a personal computer or a laptop. With the large adoption of cell phones
and tablets, it has become imperative for web pages to intuitively present themselves
on these devices too. But just proportionally shrinking a web page to fix on the screen
of the smaller device isn't the right solution as the overall display and areas
of interaction (like buttons) will be too small. Those web pages that adjust their
layouts based on the type of device reviewing the page are said to be `responsive`.

### What Is JavaScript?

JavaScript is a programming language. On web pages, it's used to do things like
respond to events (for instance, when a user clicks a picture).

#### Where Can JavaScript Code Be Found on a Web Page?

JavaScript can be found inside 'script' tag blocks on a web page.

#### How Are Variables Declared?

All programming languages use variables which store the state of different things
(like a user's bank account balance). JavaScript uses `var` to declare variables.
The `=` sign (different from `==`!) assigns a new value to the variable.

The web page below declares these variables.

```
        var ROCK = 0;
        var PAPER = 1;
        var SCISSORS = 2;
        //
        var myScore = 0;
        var computerScore = 0;
```
`ROCK`, `PAPER`, and `SCISSORS` represent a selection made by you or the computer.
These values don't change (`ROCK` is always assigned the value of `0`). Values
that don't change are known as `constants` and by convention use an all-caps name.

Values which can change (like `myScore` and `computerScore`) have names which are
all lowercase except for the first letter of each word which is capitalized.
This approach is known as `lower camel case`.

#### How Can Something Be Done But Only Under a Specific Circumstance?

JavaScript (like a lot of other languages) includes the `if/else if/else` structure
to do something under a circumstance. It must start with an `if` followed
by zero or more `else if` blocks and concluding with an optional `else` block.

The `if` and `else if` structures only execute when their respective conditions
evaluate to `true`.  If any evaluate to true, then that block's logic is executed
and the remaining `if/else if/else` structure is abandoned. If no `if/else if`
condition evaluates to `true` then the `else` block (if present) is evaluated.

Here's an example.

```
if (cloudCoveragePercentage < 10) {
    forecast = "sunny";
} else if (cloudCoveragePercentage < 40) {
    forecast = "partly cloudy";
} else if (cloudCoveragePercentage < 75) {
    forecast = "mostly cloudy";
} else {
    forecast = "cloudy";
}
```

`if`, `else if`, and `else` blocks themselves can have embedded `if/else if/else`
structures in them (which is sometimes referred to as a `nested if/else` structure).
Here's an example from the video game below - it compares your selection
with the computer's selection to determine who won and to update the score.

```
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
            ...
            } else if (mySelection == SCISSORS) {
            ...
            }
```

Note above how `==` compares two values and evaluates to `true` only if the two
values are the same.

#### What Are Functions?
Functions are bundles of reusable logic. They process submitted variables
(`input parameters`) with variables outside of functions (known as `global variables`)
and optionally respond (`return`) with a value.

Here's an example (`console.log()` is itself a predefined function which writes
text (a `string`) to the debuggers console which is helpful for developers) -
```
function addTwoNumbers(numberA, numberB) {
    return numberA + numberB;
}
console.log("5 + 7 = " + addTwoNumbers(5, 7));
```

Functions can call other functions like how the web page below declares the following
function to initialize the user's view and update the view after each round of the game.
```
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
```

##### How Are Computer Decisions Made?
Random number generators are used by programming languages to (among other things)
determine how the computer acts in a way that isn't predicable (like choosing rock,
paper, or scissors). JavaScript's `Math.random()` function generates a random decimal
from 0 up to but not including 1. Multiplying this number by a variable `range` will
generate a random decimal from 0 up to by not including `range`. The decimal part
(for the number `4.761`, the decimal part is `761`) can then be dropped with JavaScript's
`Math.floor()` function. All this can be combined to generate a random whole number
(0, 1, 2, ...) up to but not including `range`.

```
        function getRandomWholeNumberUnder(range) {
            return Math.floor(Math.random()*range);
        }
```

When `range` has the value of `3` then this function will return either 0 (for `ROCK`),
1 (for `PAPER`), or 2 (for `SCISSORS`).

##### How Is the Visual Presentation of the Web Page Updated?
The HTML page is arranged in a hierarchical structure of tags. If a tag has its
`id` attribute set, that tag can be selected with JavaScript's
`document.getElementById()` function. If an HTML image (defined by the `img` tag)
is retrieved by this function, then its `src` attribute can be changed to render
another image.

```
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
```

##### How Does JavaScript Run Based on a User Action?

HTML tags have attributes which allow actions to occur when events (like clicking
an HTML tag) happen. One such attribute is `onclick` which corresponds to the
HTML tag being clicked.

In this application, each selection (rock, paper, or scissors) has its own image
(`img` tag) which itself has an `onclick` JavaScript function to submit
the user's selection for processing.

```
                    <img class="selection_icon"
                         src="https://img.icons8.com/color/48/000000/rock.png"
                        onclick="playRockPaperScissors(ROCK)"/>
                    ...
                    <img class="selection_icon"
                         src="https://img.icons8.com/dusk/64/000000/paper.png"
                        onclick="playRockPaperScissors(PAPER)"/>
                    ...
                    <img class="selection_icon"
                         src="https://img.icons8.com/plasticine/100/000000/scissors.png"
                        onclick="playRockPaperScissors(SCISSORS)"/>

```

### What Is CSS?

CSS stands for Cascading Style Sheet and is a standard for formatting the layout
and presentation of a web page. The `style` tag includes CSS definitions.

The `<div class="wrapper">` tag used on the web page below is the outermost tag
and its `class="wrapper"` attribute horizontally centers the application (with both
`margin-left` and `margin-right` having values of `auto`), defines a fixed width
(with `width`), and puts a one-pixel solid black border around the application
(with `border`). Here is the total definition of the `wrapper` class.

```
        div.wrapper {
            width: 400px;
            margin-left: auto;
            margin-right: auto;
            border: 1px black solid;
        }
```

Other `div` (box) tags embedded in that `div` tag also have their own stylings
depending on their `class` settings. Here are some of the settings.

1. `text-align: center;` aligns everything it contains to the center
2. `width: 130px;` sets a fixed width (130 pixels in this case)
3. `display: inline-block;` allows `div` tags to be placed left-to-right instead
of top-to-bottom
4. `height: 32px;` sets a fixed height (32 pixels in this case)
5. `font-size: 36pt;` sets the font size of the text it contains
(font size of 36 point in this case)

#### How Can CSS Be Used to Make a Web Page Responsive?

Using the `@media` directive along with criteria like `max-width` instructs the web browser
to use different definitions for CSS classes based on the width of the screen. Mobile
devices have smaller widths and the use of `@media` frequently is intended for these devices.

The following directive instructs the browser to use different CSS classes when its width
is 500 pixels in length or less.

```
@media screen and (max-width: 500px)
```

For the web page below, `display: inline-block;` is used to indicate that sections (blocks)
of the web page can be arranged side-by-side (left to right), but for smaller screens
the sections should be arranged top-to-bottom so `display: block;` (which in effect
inserts an undeclared `p` (line break) after the `div` tag) is used instead. Likewise,
the font size of the title of the page changes from `font-size: 36pt;` to
`font-size: 18pt;` (it shrinks).

## Web Page Source Code

### Rock, Paper, Scissors

```
<html>
<head>
    <meta content="width=device-width, initial-scale=1" name="viewport" />
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
        @media screen and (max-width: 500px) {
            div.wrapper {
                width: 100%;
                margin-left: auto;
                margin-right: auto;
                border: 1px black solid;
            }
            div.title {
                text-align: center;
            }
            div.computer {
                display: block;
                text-align: center;
                margin-left: auto;
                margin-right: auto;
            }
            div.game {
                display: block;
                text-align: center;
                margin-left: auto;
                margin-right: auto;
            }
            div.selected_icon {
                width: 50px;
                text-align: center;
                display: block;
                margin-left: auto;
                margin-right: auto;
            }
            div.me {
                display: block;
                text-align: center;
                margin-left: auto;
                margin-right: auto;
            }
            div.selection {
                text-align: center;
            }
            div.selection_icon {
                width: 100px;
                text-align: center;
            }
            img.selection_icon {
                text-align: center;
                width: 32px;
                height: 32px;
            }
            span.title {
                font-size: 18pt;
            }
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