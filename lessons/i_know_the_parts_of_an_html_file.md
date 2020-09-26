# I know the parts of an HTML file

## Note - How to Run HTML Examples in This Lesson

For the HTML examples in this lesson, they can be implemented in the following ways.

  - Go to https://www.w3schools.com/html/tryit.asp?filename=tryhtml_basic .
    - Delete all the contents in the left text area. Paste the example contents
    into the left text area then click the 'Run >>' button.
    - The rendering of that HTML content will appear in the right area.
  - Create a local text file with a '.html' file extension (like 'sample1.html'
  as shown here). Open that file in the browser. (Either double click the file
  in a file explorer or (for Chrome) select 'File' then 'Open File' in the browser
  menu and choose the file.)
    - On Windows, do the following (to create file 'sample1.html' on the Desktop) -
      - Open a command prompt (enter `command prompt` in the Windows search bar).
      - Type command `cd %HOMEPATH%\Desktop` .
      - Type command `notepad sample1.html` .
      - In the application, enter some text, save the file, then close the application.
      - On the command prompt, type command `type sample1.html` . Confirm that what is displayed by this command exactly matches what was entered into the file.
    - On Mac, do the following (to create file 'sample1.html' on the Desktop) -
      - Open a command prompt (enter `terminal` in the Mac search bar).
      - Type command `cd ~/Desktop` .
      - Type command `touch sample1.html` . (The Unix `touch` command creates an empty file if it doesn't exist already.)
      - Type command `open -e sample1.html` .
      - In the application, enter some text, save the file, then close the application.
      - On the command prompt, type command `cat sample1.html` . Confirm that what is displayed by this command exactly matches what was entered into the file.

Note that these ways are interchangeable - implementing the example in a local file
or on a remote web site will produce the same result.

## What are HTML files?
HTML files are -the- main types of files that produce the web pages
viewed in web browsers.

## What are the files themselves?
They are a type of ... text file! The actual text consists of HTML 'tags'
and the overall layout is similar too, but not necessarily compliant with,
an XML document.

## What is XML?
XML is a way of representing data. It consists of 'tags' with each tag
starting with a word proceeded by '<' and ending with '>' and ending with
the same word proceeded by '</' and ending with '>' - other tags and text
can reside between these words. The first word can also have one or more
'attributes' with each of the form '<attribute_name>="<attribute_value>"'
assigned to it. (Ignored) Comments can be added between
a starting '<!--' and ending '-->' strings. A tag with no other tags
or text in it can be 'self-enclosing' in that it's just one word
with '<' preceeding it and ' />' trailing it - '<a></a>' can be rewritten
as '<a />' for convenience. Here's an overall example.
```
<my_mind today="February 14">
  <!-- this is a comment and therefore ignored -->
  <thoughts type="random">
    <thought>It's cold outside</thought>
  </thoughts>
  <thoughts type="organized">
    <thought>Go to work</thought>
    <thought>Buy flowers</thought>
    <thought>Take spouse out to dinner</thought>
  </thoughts>
  <thoughts type="politics" />
</my_mind>
```

While XML in general can be free-form, in specific situations
it's expected to conform to an expected standard (like in a financial
transaction).

### Exercise - Write a simple XML file
Make up some XML tags and write an un-complex XML document
describing your neighborhood. When saving the file
on your local system, make sure its filename ends in '.xml'
so that your browser knows what kind of file that it is. In Chrome,
you can view a local file by selecting the 'File' menu option
and then selecting the 'Open File' option.

## What are the sections of an HTML file?
The overall contents are encased in an 'html' tag which contains
an (optional) 'head' tag and a 'body' tag. The 'body' tag holds the
components on a page that are visible in the browser
(text, forms, lists, etc.). The 'head' tag holds updated instructions
on how the components should look (CSS - cascading style sheet)
and programming code (JavaScript) to make the page interactive
and update itself (like using AJAX - web service calls) without
reloading the entire page.

The overall structure (the 'html' tag and everything it contains)
is referred to as the 'DOM' (document object model).

## How is programming code added to a web page?
It's added in one or more 'script' tags in the 'head' tag (section).
Unless otherwise specified, these commands are interpreted to be JavaScript.
The 'alert' JavaScript command displays a pop-up message in the browser.
It's too generic and annoying to be used in Production (live) applications
but it's useful for teaching examples like here.
```
<html>
  <head>
    <script>
      alert('Hello World!');
    </script>
    <script>
      alert('Hello World Again!');
    </script>
  </head>
  <body>
    Wow, those 'alert' commands are annoying!
  </body>
</html>
```

## How is styling added to a web page?
It's added in one or more 'style' tags in the 'head' tag (section).
All tags of a certain kind, specific classes of a tag (identified
by the 'class' attribute), and specific instances of a tag (identified
by the 'id' attribute - at most one tag on a web page should have
a specific 'id' value).

How the 'style' tag declarations define styling is governed
by the CSS (Cascading Style Sheet) specification.

In this example, the 'p' tag represents a paragraph.

```
<html>
  <head>
    <style>
      p {
        font-size: 18pt;
      }
      p.blue_text {
        color: blue;
      }
      p#C {
        font-style: italic;
      }
    </style>
  </head>
  <body>
    <p id="A">All paragraphs have large text</p>
    <p id="B" class="blue_text">Some paragraphs have blue text</p>
    <p id="C" class="blue_text">Just this paragraph has italized text</p>
  </body>
</html>
```

## How are visible components and text added to a web page?
They are added as tags within the 'body' tag. And those tags can themselves
have tags within them. Text can reside within a tag too.

## Can an individual tag be uniquely identified?
Yes, each HTML tag supports the optional 'id' attribute
which should have a unique value. Both JavaScript and CSS
can search for this unique value to interact with and style
that specific tag.

## What are commonly used components?

Here are several commonly used HTML tags.

### p
This demarcates a paragraph. Pressing the 'return' key does not
create a new line in HTML (it just creates another space).
When this tag doesn't contain anything (text or tags), it's about
equivalent to two 'return' keys. When it contains text and/or tags,
those things will be prepended and appended with empty lines (about
two 'return' keys').

```
<html>
  <body>
    Hello
    <p />
    Hi
    <p>
    Good morning to you
    </p>
    Be well
  </body>
</html>
```

### br
This is like the 'p' tag but it create about half the vertical spacing
(like pressing the 'return' key once).

```
<html>
  <body>
    Line One
    <br />
    Line Two
    <br>
    Line Three
    </br>
    Line Four
  </body>
</html>
```

### hr
Renders a horizontal bar.

```
<html>
  <body>
    Above the line
    <hr />
    Below the line
  </body>
</html>
```

### div
Wraps a section of HTML content (both tags and text) into a common
block for styling (like applying a border). By its default behaviour,
it's like a 'p' tag but much more purposefully used by web UI
developers to define the layout of a page (like menus and footer).
It's quite common for a web page to have 'div' tags immediately
below the 'body' tag in the DOM hierarchy. This tag is heavily
used by web UI developers because of its styling flexibility.

```
<html>
  <head>
    <style>
      div {
        border: 1px solid black
      }
    </style>
  </head>
  <body>
    <div>Content in a box
    </div>
  </body>
</html>
```


### span

This is like a 'div' tag but doesn't block itself out. It's used more
for inline styling (usually for text). This is used frequently.

```
<html>
  <head>
    <style>
      span {
        color: green;
        font-size: 14pt;
      }
    </style>
  </head>
  <body>
    Oh, it's March 14? <span>Happy Saint Patrick's Day!</span>
  </body>
</html>
```

### ul
Creates a list of bullet points with each bullet point
represented by a nested 'li' tag.

```
<html>
  <body>
    Healthy Snacks
    <ul>
      <li>Apple</li>
      <li>Pear</li>
      <li>Orange</li>
    </ul>
  </body>
</html>
```

### ol
Creates numbered list with with each numbered items
represented by a nested 'li' tag.

```
<html>
  <body>
    Follow these steps to retire early
    <ol>
      <li>Get a high-paying job</li>
      <li>Live well below your means</li>
      <li>Invest your savings well</li>
    </ol>
  </body>
</html>
```

### li
Represents an item within a list (created by either a 'ul' tag or an 'ol' tag).

### iframe
Creates a block that displays another web page in it.
The value of the 'src' attribute determines which web page to display.

### a
Creates a hyperlink with the 'href' attribute being the destination.
Including the optional 'target' attribute with the value '_blank'
will open up a new browser window.

```
<html>
  <body>
  Favorite News Sites
  <ul>
    <li><a href="https://www.usatoday.com">USA Today</a></li>
    <li><a href="https://www.cnn.com">CNN</a></li>
    <li><a href="https://www.foxnews.com">FoxNews</a></li>
    <li><a href="https://www.nbcnews.com">MSNBC</a></li>
    <li><a href="https://news.google.com" target="_blank">Google News (another window)</a></li>
  </ul>
  </body>
</html>
```

### table
Used to create a table (rows and columns). For generalized web page
layout (like a page including a header and a footer), 'div' tags
are generally used instead.

Tables are good for an actual rigid table structure in a page.
A row is declared (top to bottom) with the 'tr' tag and each cell
(arranged left to right) of each row is declared with the 'td' tag.

```
<html>
  <body>
    Travel Destination Chart
    <table>
      <tr>
        <td>City</td>
        <td>Weather</td>
        <td>Expensive</td>
      </tr>
      <tr>
        <td>Tokyo</td>
        <td>Temperate</td>
        <td>Quite</td>
      </tr>
      <tr>
        <td>St. Petersberg</td>
        <td>Cold</td>
        <td>Affordable</td>
      </tr>
      <tr>
        <td>Cape Town</td>
        <td>Temperate</td>
        <td>Affordable</td>
      </tr>
      <tr>
        <td>Orlando</td>
        <td>Hot</td>
        <td>Somewhat</td>
      </tr>
      <tr>
        <td>Rio De Jinero</td>
        <td>Quite</td>
        <td>Cheap</td>
      </tr>
      <tr>
        <td>Sydney</td>
        <td>Temperate</td>
        <td>Somewhat</td>
      </tr>
      <tr>
        <td>South Pole</td>
        <td>Incredibly Cold!</td>
        <td>Prohibative</td>
      </tr>
    </table>
  </body>
</html>
```

### img
Displays a block with an image in it. The image is referenced
by the 'src' (source) attribute. This attribute's value can either be
a file in the same directory as the web page, a file in a subdirectory
relative to this web page, a file located elsewhere but on the same
web server, or a file on another web server.

Here are possible values for the 'src' attribute for different
locations of the web page.

- Same Directory - 'image1.jpeg'
- Subdirectory - 'images/picture2.gif'
- Same Web Server, Different Directory - '/media/caption3.jpg'
- Different Web Server - 'https://some.picture.com/artwork4.png'

```
<html>
  <body>
  Here's a cool castle
  <p />
  <img src="https://www.si.edu/sites/default/files/historic-castle-400.jpg" />
  </body>
</html>
```

### video
Displays a block with a video clip in it. The video is referenced
by the 'src' (source) attribute.

### audio
Displays a block with an audio clip in it. The audio is referenced
by the 'src' (source) attribute.

### h1, h2, h3, ...
Displays stylized headers in the web page. The smaller the number
used in the tag's name, the bigger the header ('h1' is the biggest).

```
<html>
  <body>
    <h1>Scientific Genius</h1>
    <h2>Chapter 1</h2>
    An apple hit Isaac Netwon on the head.
    <h2>Chapter 2</h2>
    Isaac Newton conceptualized the theory of gravity.
  </body>
</html>
```

## What are forms?
Forms are groupings of interactive components
(like buttons, text boxes, and drop-down menus) that a user
can adjust and submit. For very traditional web sites,
this is -the- way that a user submits information
(like placing an order).

### How are forms demarcated?
All forms are enclosed by a 'form' tag. Two common attributes
assigned to this tag are 'action' (URL indicating where the form
should be submitted) and 'method' (usually 'POST' is used for
'important' things involving sensitive data and financial transactions,
but 'GET' can be used for casual and less sensitive submissions).

### What are commonly used form tags?
Some form tags are listed below. Each uses the 'name' attribute
which is sent to the server along with its corresponding value
once the form is submitted.

#### select
Displays a dropdown or multi-select list. One or more 'option'
tags determine which values can be selected. For dropdowns, the
topmost 'option' tag is the one first selected unless another
'option' tag has the 'selected' attribute with 'true' for its value.
The value in the selected option's 'value' attribute is what
gets sent to the server on form submission. The text in the 'option'
tag is what gets displayed for that option.

```
<html>
  <body>
    <form>
      <select name="favoriteColor">
        <option value="red">Red</option>
        <option value="blue">Blue</option>
        <option value="yellow">Yellow</option>
        <option value="purple">Purple</option>
        <option value="green" selected="true">Green</option>
        <option value="orange">Orange</option>
      </select>
    </form>
  </body>
</html>
```

#### input
Represents a block of text that should be submitted with the form.

##### type="text"
Displays an unconcealed block (single line) of text.

```
<html>
  <body>
    <form>
      Username: <input type="text" name="username">Joe</input>
    </form>
  </body>
</html>
```

##### type="password"
Displays a concealed block (single line) of text.

```
<html>
  <body>
    <form>
      Secret Code: <input type="password" name="secret"></input>
    </form>
  </body>
</html>
```

##### type="hidden"
Represents a text value hidden from view. This is often used in form
submissions to send a fixed value that the browser user shouldn't change
(maybe like the user's home address, like, for instance, if the user
checks 'Use my home address' checkbox when submitting an order).

```
<html>
  <body>
    <form>
      <input type="hidden" name="useHomeAddress">true</input>
    </form>
  </body>
</html>
```

#### textarea
Displays an unconcealed multi-line block of text.

```
<html>
  <body>
    <form>
      <textarea name="poem">
      When I look outside,
      I see flowers in my eyes
      Now I know it's spring
      </textarea>
    </form>
  </body>
</html>
```

## Exercise - Write a simple web page
Using the HTML tags on this page, write an un-complex web page
about something you are interested (like a hobby). When saving the file
on your local system, make sure its filename ends in '.html'
so that your browser knows what kind of file that it is. In Chrome,
you can view a local file by selecting the 'File' menu option
and then selecting the 'Open File' option.

## Exercise - Study a web page
In a Chrome browser, go to https://www.si.edu
(the Smithsonian Institution's official web site), right-click over
the page, and select the 'View Page Source' option. In that tab,
study the HTML.

### Bonus - Study the DOM Structure
Go back to the page, right-click over the page, and select the 'Inspect'
option. This will bring up Chrome's DevTools which web UI developers
very frequently use during development and troubleshooting. Make sure
the 'Elements' tab is selected. Study the hierarchical nature
of the DOM structure. Notice how the 'div' tag is used to organize
sections of the page.

### Double Bonus - Change the DOM Structure
In the 'Elements' pane, right-click over an HTML tag and select
the 'Delete element' option and note how that element disappears
from the viewable page. I've used this technique to remove ads
and pay walls from web pages.
