# Bonus: I Have Used the Online Authoring Tool to Create a Simple Game

## How to Create Images

Go to https://jspaint.app/ or use the local Windows 'Paint' program to create
two images - the 'head' side of a coin and the 'tail' side of a coin.

### Set Dimension Boundaries and (Optionally) Make the Background Transparent

In the menu, click 'Image' then 'Attributes' then do the following.

  - For 'Units', select 'Pixels'
  - For 'Width', enter the desired width (like 100) in pixels
  - For 'Height', enter the desired height (like 100) in pixels
  - (Optional) To make sure that the unpainted parts of the image don't cover
  up what's behind it, select 'Transparent' under 'Transparency'

Once this is done, click the 'Okay' button.

  - If you selected the 'Transparency' button, clear the existing (white) background
  by selecting 'Image' then 'Clear Image' . The image should now look somewhat like
  a checkerboard (this is the representation of a transparent background,
  but it (the unpainted parts) will be 'see through' once rendered on a web page).

### Create Two Images - One of the Head Side of a Coin, One of the Tail Side of a Coin

Create two images - one of the head side of a coin, one of the tail side of a coin.

These images should be your artistic creation and does not have to represent
an actual coin in real life.

These images will have to be created one-at-a-time.

Save each file by clicking 'File' then 'Save' . Each saved file will have the name
'untitled.png' but should be named 'heads.png' and 'tails.png' for the head side and
tail side, respectively.

After saving the first image, click 'File' then 'New' to reset the canvas to start
working on the second image (don't forget to reset the boundaries and (optionally)
choose to enable transparency).

### Create 'CoinFlipGame.html' File
Create a file named 'CoinFlipGame.html' with the following content.

```
<html>
    <head>
        <script src="/jquery-3.5.1.min.js"></script>
        <script src="/commonUtils.js"></script>
        <script>
            var author = 'garysteinmetz';
            var game = 'coinflipgame';
            var allPlayerData = [];
            var user;
            var topScore = -1;
            var lastGameScore = -1;
            var score = 0;
            function flipCoin() {
                var flipResult = getRandomWholeNumberUnder(2);
                if (flipResult === 1) {
                    $("#coin_flip").attr("src", "heads.png");
                    score++;
                } else {
                    $("#coin_flip").attr("src", "tails.png");
                    lastGameScore = score;
                    score = 0;
                    if (lastGameScore > topScore) {
                        topScore = lastGameScore;
                        if (user && user.isLoggedIn) {
                            sendData(author, game, {score: topScore}, null);
                        }
                    }
                }
                updateHighScores();
            }
            function updateHighScores() {
                var highScoresEle = $("#high_scores");
                $(highScoresEle).empty();
                //
                if (lastGameScore >= 0) {
                    var span1 = document.createElement( "span" );
                    $(highScoresEle).append(span1);
                    $(span1).text("The score of your last game was " + lastGameScore);
                    var br1 = document.createElement( "br" );
                    $(highScoresEle).append(br1);
                }
                if (topScore >= 0) {
                    var span2 = document.createElement( "span" );
                    $(highScoresEle).append(span2);
                    $(span2).text("Your best-ever score is " + topScore);
                    var br2 = document.createElement( "br" );
                    $(highScoresEle).append(br2);
                }
                var span3 = document.createElement( "span" );
                $(highScoresEle).append(span3);
                $(span3).text("The score of your current game is " + score);
                var br3 = document.createElement( "br" );
                $(highScoresEle).append(br3);
                //
                var h2 = document.createElement( "h2" );
                $(highScoresEle).append(h2);
                //$(a).attr("href", href);
                $(h2).text("High Scores");
                for (var i = 0; i < allPlayerData.length && i < 5; i++) {
                    var div = document.createElement( "div" );
                    $(highScoresEle).append(div);
                    $(div).text(allPlayerData[i].score + " - " + allPlayerData[i].username);
                }
            }
            function downloadHighScoresAndUpdateHighScores() {
                updateHighScores();
                /*
                $.get(
                    {
                        url: "/appState/" + author + "/" + game + "/allUsers",
                        success: function(data, status) {
                        console.log("YYY");
                        console.log(data);
                            var players = Object.keys(data);
                            for (var i = 0; i < players.length; i++) {
                                var nextPlayer = data[players[i]];
                                console.log("ZZZ");
                                console.log(nextPlayer);
                                var playerData = {
                                    username: nextPlayer,
                                    score: data[nextPlayer].app_data.score
                                };
                                allPlayerData.push(playerData);
                                allPlayerData.sort(
                                    function(a, b) {
                                        return (b.score > a.score) ? 1 : -1;
                                    }
                                );
                            }
                            //allPlayerData = data;
                            updateHighScores();
                        }
                    }
                );
                */
            }
            $( document ).ready(
                function() {
                    getUserInfo(
                        function(data, status) {
                            generateLoginDomStructureImpl("user_pane", data);
                            if (data.isLoggedIn) {
                                user = data;
                                getData(author, game,
                                    function(data, status) {
                                        if (data.isPresent) {
                                        console.log("ZZZ");
                                        console.log(data);
                                            var appData = JSON.parse(JSON.parse(data.appData));
                                            if (appData.score) {
                                                topScore = appData.score;
                                                downloadHighScoresAndUpdateHighScores();
                                            }
                                        }
                                    }
                                );
                            } else {
                                downloadHighScoresAndUpdateHighScores();
                            }
                        }
                    );
                }
            );
        </script>
    </head>
    <body>
        <div style="align: center">
            <h1>Coin Flip Game</h1>
            <div style="align: center">
                Try to get as many consecutive 'heads' flips as you can!
            </div>
            <hr />
        </div>
        <div id="user_pane"></div>
        <div id="high_scores" style="align: center">
        </div>
        <div>
            <hr />
            <input type="button" onclick="flipCoin()" value="Flip Coin!" />
            <br />
            <img id="coin_flip" src="" />
            <br />
        </div>
    </body>
</html>
```