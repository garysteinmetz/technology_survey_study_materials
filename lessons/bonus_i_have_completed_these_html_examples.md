# Bonus: I Have Completed These HTML Examples

The examples below work as full HTML pages.

Normally, these samples can be copy-pasted into a text editor, saved
as a file (with filename ending in '.html'), then opened with a browser.

Alternatively, and for convenience, you can instead go to
https://www.w3schools.com/html/tryit.asp?filename=tryhtml_basic ,
copy-paste the HTML into the left pane, click the "Run >>" button,
then confirm the results in the right pane.

## Create a List for Baking a Cake

The example below uses the 'ol' HTML tag to present a numbered
list of steps to bake a cake.

```
<html>
    <body>
        <ol>
            <li>Buy Flour</li>
            <li>Mix Flour with Water</li>
            <li>Turn On Oven</li>
            <li>Place Flour Mix in Pan, Then Place Pan in Oven</li>
            <li>Wait Until Flour Is Baked, Then Remove from Oven</li>
            <li>Turn Off Oven</li>
            <li>Placed Baked Flour (Now a Cake) on Plate</li>
            <li>Place Icing on Cake</li>
            <li>Clean Up Baking Equipment</li>
        </ol>
    </body>
</html>

```

## Catch the Cheese

This web page just displays an image of cheese that moves whenever
the mouse goes over it. Adjusting the window also moves the cheese
(for the case the user adjusts (shrinks) the browser and the cheese
is no longer viewable).

The 'getRandomWholeNumberUnder' function is used to generate random
numbers which 'moveCheese' uses to determine the new location
of the cheese on the page. 'cheeseIcon.style.left' and 'cheeseIcon.style.top'
are used by JavaScript to assign the new position of the cheese.

CSS value 'position: fixed' states that the coordinates of the cheese
should be relative to the entire HTML page (not the parent HTML
element that contains it).

```
<html>
    <head>
        <script>
            var cheeseImageWidth = 48;
            var cheeseImageHeight = 48;
            function getRandomWholeNumberUnder(range) {
                return Math.floor(Math.random()*range);
            }
            function moveCheese() {
                //get the HTML element representing the cheese image
                var cheeseIcon = document.getElementById("cheese");

                //get scrollbar settings - for this app both values are probably 0
                //  reference - from https://plainjs.com/javascript/styles/get-and-set-scroll-position-of-an-element-26/
                var scrollLeft = window.pageXOffset || document.documentElement.scrollLeft;
                var scrollTop = window.pageYOffset || document.documentElement.scrollTop;

                //get the new position of the cheese
                //  reference - https://www.w3schools.com/jsref/prop_win_innerheight.asp
                //  use 'cheeseImageWidth/cheeseImageHeight' to factor in the width/height
                //    of the cheese so that all of the cheese appears in the browser's window
                //      (otherwise, there's a risk that part of the cheese will be outside of window
                var leftOffset = getRandomWholeNumberUnder(window.innerWidth - cheeseImageWidth);
                var topOffset = getRandomWholeNumberUnder(window.innerHeight - cheeseImageHeight);

                //
                cheeseIcon.style.left = (scrollLeft + leftOffset) + "px";
                cheeseIcon.style.top = (scrollTop + topOffset) + "px";
            }
        </script>
        <style>
            img.cheese {
                width: 48px;
                height: 48px;
                position: fixed;
            }
        </style>
    </head>
    <!-- Use 'onresize' event to move cheese if user changes window size or scrollbar settings -->
    <body onresize="moveCheese()">
        <!-- Move cheese whenever mouse touches it -->
        <img id="cheese" class="cheese" onmouseover="moveCheese()"
             src="https://img.icons8.com/doodle/48/000000/cheese--v1.png"/>
        <script>
            //set initial positioning of cheese
            moveCheese();
        </script>
    </body>
</html>
```

## Cartoon Strip

```
<html>
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script>
      //var imageHeight = 200;
      //var imageWidth = 300;
      //Note - Use website like 'https://jspaint.app/' to create images used by 'images' variable immediately below
      var images = ["heads.png", "tails.png", "z.png"];
      var captions = ["Heads!", "Tails!", "Neither!"];
      var captionStyles = ["style0", "style1", "style2"];
      function initialize() {
        var errorFound = (images.length !== captions.length || captions.length !== captionStyles.length);
        if (!errorFound) {
          for (var i = 0; i < images.length; i++) {
            var innerFrame = $("<div/>");
            $(innerFrame).attr("id", "frame" + i);
            $(innerFrame).attr("class", "innerFrame");
            $("#frameContainer").append(innerFrame);
            //
            var img = $("<img/>");
            $(img).attr("id", "image" + i);
            $(img).attr("src", images[i]);
            if (typeof imageHeight !== "undefined") {
              $(img).attr("height", imageHeight);
            }
            if (typeof imageWidth !== "undefined") {
              $(img).attr("width", imageWidth);
            }
            $(innerFrame).append(img);
            //
            var br = $("<br/>");
            $(innerFrame).append(br);
            //
            var span = $("<span/>");
            $(span).attr("id", "text" + i);
            $(span).text(captions[i]);
            $(span).attr("class", captionStyles[i]);
            $(innerFrame).append(span);
          }
          //Each loop in the 'for loop' above should produce an HTML block like the following
          //  <div id="frame0" class="innerFrame">
          //    <img id="image0"/>
          //    <br />
          //    <span id="text0" />
          //  </div>
        } else {
          alert("Setup is not correct!");
        }
      }
      $(document).ready(
        function() {
          initialize();
        }
      );
    </script>
    <style>
      body {
        align: center;
      }
      .outerFrame {
        border: 1px solid black;
        align: center;
        display: flex;
      }
      .innerFrame {
        border: 1px dashed black;
        flex: 1;
        text-align: center;
      }
      .fadeOutInTwoSeconds {
        transition: visibility 0s 2s, opacity 2s linear;
        visibility: hidden;
        opacity: 0;
      }
      /*
        Note - Customize Below (especially those CSS classes beginning with 'style')
          Refer to 'color' values for text at https://htmlcolorcodes.com/color-chart/
          Refer to 'font-family' values for text at https://www.w3schools.com/cssref/css_websafe_fonts.asp
      */
      .style0 {
        font-family: Serif;
        color: #FF0000;
        font-size: 22pt;
      }
      .style1 {
        font-family: Sans-Serif;
        color: #00FF00;
        font-size: 16pt;
      }
      .style2 {
        font-family: Monospace;
        color: #0000FF;
        font-size: 18pt;
      }
    </style>
    <script>
      //here's a fun function that causes the comic strip to disappear in two seconds
      function fadeOutCartoon() {
        $("#frameContainer").addClass("fadeOutInTwoSeconds");
      }
    </script>
  </head>
  <body>
    <div id="frameContainer" class="outerFrame" onclick="fadeOutCartoon();">
    </div>
  </body>
</html>
```