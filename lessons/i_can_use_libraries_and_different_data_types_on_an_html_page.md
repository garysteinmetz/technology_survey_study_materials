# I Can Use Libraries and Different Data Types of an HTML Page

## Data Types

Data types are a fundamental building block of programming languages
(like JavaScript). They represent nouns. Like nouns can be persons,
places, things, or ideas, one data type (like the location Tokyo)
can be completely different from another (like a form of government,
like monarchy) and can't be compared to each other.

### Common JavaScript Data Types

In JavaScript, variables are declared with the `var` keyword. Unlike
other (`typed`) languages where the variable declaration explicitly states
the kind of data type (like `int bankBalance = 200;` in Java explicitly
declares an integer with a value of 200, `int bankBalance = "Giraffe";`
is an illegal command in Java and won't be accepted).
JavaScript is `untyped` which means that any `var` value can be
assigned any data type, even if resetting the `var` completely changes
its meaning. Here's an example of valid JavaScript -
```
//all of these commands are valid JavaScript
var bankBalance = 200;
bankBalance = "giraffe";//bank balances can't be animals
bankBalance = true;//what does that mean?
bankBalance = ['A', 'B', 'C'];//bank balances can't be the alphabet
bankBalance = {"name": "Bob"};//bank balances can't be people
```

There is lively informal debate within the software development community
as to whether a `typed` language is better (more discipline?)
or worse (`'too much ceremony'`?) than an `untyped` language.

#### Boolean
Booleans are arguably the simplest data type. They normally just
have a value of `true` or `false` which can be used to make logical
`yes/no` evaluations that a program (like a web application)
uses to make decisions. Here is an example.

```
var raining = true;
if (raining) {
  bringUmbrella();
}
if (raining == false) {
  wearSunglasses();
}
```

##### Not Operator

The Not operator (`!`) inverts a logical evaluation converting `true`
to `false` and `false` to `true`. Here's an example.
```
var raining = false;
if (!raining) {
  wearSunglasses();
}
```

##### Truthy/Falsey

In JavaScript, not only is `false` interpreted as false in logical
statements, these other values are also interpreted as false
in logical statements - `0`, `null`, `undefined`, `''` (that's a string
of exactly zero characters), `NaN` (not-a-number - which doesn't
occur that often
(like trying to convert a non-number string to a number)).

Everything else is interpreted as `true`. Here are examples.
(To see the output, before loading the page,
(in Chrome on Mac) press and continue to hold
down both the `Command` and `option` buttons then press the letter `i`
then click the `Console` tab in the developer tools window.)

```
<html>
    <head>
        <script>
            //the numbers 1 through 12 will be printed
            var something;//this is undefined
            if (!something) {
              console.log(1);
            }
            something = null;
            if (!something) {
              console.log(2);
            }
            something = false;
            if (!something) {
              console.log(3);
            }
            something = '';
            if (!something) {
              console.log(4);
            }
            something = parseInt("blabla");
            if (!something) {
              console.log(5);
            }
            something = Math.sqrt(-1);
            if (!something) {
              console.log(6);
            }
            something = true;
            if (something) {
              console.log(7);
            }
            something = -1;
            if (something) {
              console.log(8);
            }
            something = ' ';
            if (something) {
              console.log(9);
            }
            something = 'Giraffe';
            if (something) {
              console.log(10);
            }
            something = {"name": "Yin"};
            if (something) {
              console.log(11);
            }
            something = ['A', 'B', 'C'];
            if (something) {
              console.log(12);
            }
        </script>
    </head>
</html>
```

`Typed` languages like Java don't allow values other than
`true` or `false` in logical evaluations.

##### Compound Logical Evaluations

###### Compound OR

Sometimes multiple things are checked before logic is executed.
Both `|` (pipe character) and `||` represent a logical `OR` meaning
that if either condition evaluates to true then the logic is executed.
`||` has the additional feature of not evaluating the right term
if the left term is true (this is often quite useful for avoiding
situations where an object isn't defined).

Here are examples for `|`.
```
var bakingCake = false;
var bakingMuffins = true;
if (bakingCake | bakingMuffins) {
    turnOnStove();
}
//Note - the following will throw an error because
//  'car' isn't defined so checking 'gasTankFull' doesn't make sense
//  use '||' instead
var car;
if (!car | car.gasTankFull) {
    dontGoToGasStation();
}
```

Here are examples for `||`.
```
var bakingCake = false;
var bakingMuffins = true;
if (bakingCake || bakingMuffins) {
    turnOnStove();
}
//Note - the following will Not throw an error because
//  'car.gasTankFull' won't be evaluated
var car;
if (!car || car.gasTankFull) {
    dontGoToGasStation();
}
car = {"gasTankFull": true};
if (!car || car.gasTankFull) {
    dontGoToGasStation();
}
```

####### Bonus - Compound OR for Variable Initialization

For advanced web applications, like where libraries are being loaded,
the `||` operator can be used to set a default value if a value
hasn't already been set. Here's an example.

```
var greeting = greeting || "Hello";

```
If `greeting` had been previously set (like to `Good Morning`),
then it doesn't get the value of `Hello`.

###### Compound AND
Both `&` (ampersand character) and `&&` represent a logical `AND` meaning
that both conditions must evaluate to true for the logic to be executed.
`&&` has the additional feature of not evaluating the right term
if the left term is false (this is often quite useful for avoiding
situations where an object isn't defined).

Here are examples for `&`.

```
var sunny = true;
var hot = true;
if (sunny & hot) {
    putOnSunTanLotion();
}
//Note - the following will throw an error because
//  'car' isn't defined so checking 'gasTankFull' doesn't make sense
//  use '&&' instead
var car;
if (car & car.gasTankFull) {
    dontGoToGasStation();
}
```

Here are examples for `&&`.
```
var sunny = true;
var hot = true;
if (sunny && hot) {
    putOnSunTanLotion();
}
//Note - the following will Not throw an error because
//  'car.gasTankFull' won't be evaluated
var car;
if (car && car.gasTankFull) {
    dontGoToGasStation();
}
car = {"gasTankFull": true};
if (car && car.gasTankFull) {
    dontGoToGasStation();
}
```

#### Number
Numbers are numbers - either integers or numbers with decimal points.
Here are examples.
```
var bankBalance = 200;
//withdrew money, lower bank balance
bankBalance = 190.5;
```

##### Arithmetic
The operators `+`, `-`, `*`, and `/` correspond to the arithmetic
operations add, subtract, multiply, and divide, respectively.
Here are examples.
```
var bankBalance = 150 + 50.5;//200.5
bankBalance = bankBalance - 0.5;//200
bankBalance = bankBalance*2;//400
bankBalance = bankBalance/40;//10
```

##### Number Comparisons
Numbers can be compared to each other to generate true/false results
for logical evaluation. `==`, `!=`, `<`, `>`, `<=`, `>=` correspond
to the logical evaluations equal to, not equal to, less than, greater than,
less than or equal to, and greater than or equal to, respectively.

Here are examples.
```
var bankBalance = 200;
//all of these evaluate to true
var result = (bankBalance == 200);
result = (bankBalance != 201);
result = (bankBalance < 400);
result = (bankBalance > 199);
result = (bankBalance <= 200);
result = (bankBalance <= 201);
result = (bankBalance >= 200);
result = (bankBalance >= 199.99);
```

##### 'Math' Object
JavaScript includes a `Math` object for advanced math operations.
Here are examples.
```
var n;
n = Math.PI;//3.141592653589793
n = Math.round(4.4);//4
n = Math.round(4.7);//5
n = Math.pow(8,2);//8*8=64
n = Math.floor(4.999);//4

```

##### 'parseFloat' Function
JavaScript has a `parseFloat` function for converting strings to numbers.
Invalid input results in `NaN` as a response value. Here are examples.
```
var n = parseFloat("5.5");//5.5
n = parseFloat("HahHahInvalid");//NaN
```

#### String
Strings are an ordered sequence of characters. Characters can include
letters, numbers, punctuation, symbols, and something called `whitespace`.
Whitespace represents characters that adjust the layout of a string
and they include things like spaces (' '), tabs, and the enter/return
character (actually, on Windows, it's represented as two characters -
'carriage return' and 'line feed').

String values can be encased with either matching single quotes (`'`)
or matching double quotes (`"`).

Strings can be concatenated together to form a single composite
string using the `+` operator. Likewise, strings and non-strings
can be concatenated together to form a single composite string the same way.
Here are examples.
```
var s = "abc" + "xyz";//"abcxyz"
s = "a" + null + "b" + false + "c" + 5;//"anullbfalsec5"
```

##### String Functions
The `length` member variable and supporting functions can be useful
when interacting with strings. The first character in a string is
actually the zeroth (not first) character. Here are examples.

```
var s = " abc xyzz  ";
console.log(s.length);//11
console.log(s.trim();//"abc xyzz" - remove leading/trailing whitespace
console.log(s.replace("a", "q);//" qbc xyzz  "
console.log(s.substr(1,3));//"abc" - get three characters starting with first
console.log(s.indexOf("xyz"));//5 - get index of first occurrence or -1 if not found
console.log(s[1]);//"a" - get character at index 1
console.log(s.split("c"));//[" ab", " xyzz  "] - splits string by pattern
```

#### Date

The date data type is useful for getting time values and determining
how much time has passed. Here are examples for creating a date object
and getting elapsed time. (`UTC` refers to a standard international
time zone (corresponding to England with daylight saving time adjustments.)
```
var d = new Date();//current date/time
var elapsedTime = d.getTime();//number of milliseconds since January 1, 1970 00:00:00 UTC
```

#### Undefined and Null
Uninitialized variables are by default assigned a value of `undefined`
while a variable can explicitly be assigned no value with `null`.
```
var middleName;//has undefined value
middleName = null;//the person has no middle name
if (middleName == null) {
    console.log("This person has no middle name");
}
```

#### Array
An array is a sequential listing of zero or more items.
(In JavaScript,) Each item in an array can be of any data type
(including null). Like a string, the first element of an array
is actually the zeroth element. Here's an example.

```
var shoppingList = ['apples', 'milk', 'pizza'];
var fruits = shoppingList[0];//'apples'
var dairy = shoppingList[1];//'milk'
var junkFood = shoppingList[2];//'pizza'
```

##### Array Functions
JavaScript supports a number of array functions including the following.

```
var shoppingList = ['apples', 'milk', 'pizza'];
var numberOfItems = shoppingList.length;//3
var zerothItem = shoppingList[0];//'apples'
shoppingList.push('celery');//add item to end of array
var vegetable = shoppingList.pop();//remove item from end of array
var firstItem = shoppingList.indexOf('milk');//1
```

#### Object
Informally speaking in JavaScript, objects are 'amalgamations'
(collections) of things. Objects consist of zero or more properties
(known as `key-value pairs`). Each property (key) has a name
(usually it's a string) and that property is assigned a value.
Property values can be of any data type - including booleans, numbers,
strings, and arrays even functions and other objects.

Here's an example.
```
var verySimpleObject = {};//this object has no keys!
var person = {
  "name": "Prince Harry",
  "hairColor": "red",
  "isWorkday": function(dayOfWeek) {
    return (dayOfWeek != "Saturday" && dayOfWeek != "Sunday");
  },
  "royalty": true,
  "yearOfBirth": 1984,
  "siblings": [
    {
      "name": "Prince William"
    }
  ]
};
var dayOfWeek = "Wednesday";
//Hello, my name is Prince Harry and I have red hair.
console.log("Hello, my name is " + person.name
  + " and I have " + person.hairColor + " hair.");
//I am royalty. I was born in 1984 and have 1 sibling(s).
console.log("I " + ((person.royalty)? "am" : "am not") + " royalty."
  + " I was born in " + person.yearOfBirth + " and have "
  + person.siblings.length + " sibling(s).");
//Since today is Wednesday, I will be working.
console.log("Since today is " + dayOfWeek
  + ", I will" + ((person.isWorkday(dayOfWeek))? "" : " not")
  + " be working.");
```

The `(A)? B : C` notation means if A is true then return B otherwise
return C.

The keys of an object can be gotten (as a list) using the `Object.keys()`
call which is demonstrated below (continuing the example above).
```
var personAttributes = Object.keys(person);
console.log("I can tell you about the following about me, "
  + person.name + ".");
for (var i = 0; i < personAttributes.length; i++) {
  console.log("  - " + personAttributes[i]);
}
//I can tell you about the following about me, Prince Harry.
//  - name
//  - hairColor
//  - isWorkday
//  - royalty
//  - yearOfBirth
//  - siblings
```

##### Prototype
JavaScript allows you to create your own object types.

It's a complicated subject, but here's a brief example.
```
function Person(name) {this.name = name};
Person.prototype = {
    print: function() {return this.name;}
};

var personOne = new Person("Prince Harry");
console.log(personOne.print());
var personTwo = new Person("Prince William");
console.log(personTwo.print());
```

#### Function
Functions are like verbs - they do things. What they do and how they
do it frequently is determined by what `arguments` it receives.
Functions can optionally `return` a value which the caller can
optionally use. Here are examples.

```
//this function just takes one input argument ('message')
//  and doesn't return anything
function saySomething(message) {
  console.log(message);
}
saySomething("Hey there");
//this function takes two arguments ('numberOne' and 'numberTwo')
//  and returns their sum
function addNumbers(numberOne, numberTwo) {
  return numberOne + numberTwo;
}
saySomething('Uno - ' + addNumbers(1, 0));
saySomething('Dos - ' + addNumbers(1, 1));
saySomething('Tres - ' + addNumbers(1, 2));
//
//functions can also be assigned directly to a variable
var subtractOne = function(number) {return number - 1};
saySomething("1 - 1 = " + subtractOne(1));
```

##### Arrow Functions
More recently, a more streamlined way of declaring a function
is now available and has become popular. It's known as an `arrow function`
and is of the form `(argumentList) => {actions}`. It has two major benefits.

1) It removes the need to type the `function` keyword. Even the curly
braces (`{` and `}`) are optional if there is only one action and
its value is what the function should return.
2) (This is important.) The `this` keyword always has an unambiguous
value. The traditional use of `this` in `function` has not been consistent.
(The definition and explanation of the `this` keyword is beyond
the scope of this introductory overview, but it's an important topic
for JavaScript developers.)

Here are examples.
```
var alwaysReturnOne = () => 1;
console.log('This most definitely should be one - ' + alwaysReturnOne());
var addTwoNumbers = (numberOne, numberTwo) => (numberOne + numberTwo);
console.log('Adding one and one should most definitely be - ' + addTwoNumbers(1, 1));
```

#### Regular Expressions
Regular expressions (often referred to as `reg ex`) are search patterns.
Normal string functions are not conveniently malleable in the way
that regular expressions are. They can be used to find -

1) Where in a string a pattern can be found
2) If a string conforms to an overall pattern

Here's a quick example that removes all whitespace from a string.
```
var str = " a b   c  d       ";
//In regular expression '/\s/g', '\s' means all white space
//  and 'g' means 'greedy' (replace each whitespace character
str = str.replace(/\s/g, '');
console.log(str);//'abcd'
```

Here's a quick example to check if a string starts with 'hello' -
web page JavaScript frequently uses regular expressions to validate
user input (like to determine if a user entered a correctly-formed
email address).
```
var regEx = /^hello/;
var strOne = 'hello there';
var resultOne = regEx.test(strOne);//true
console.log(resultOne);
var strTwo = 'hi and good morning';
var resultTwo = regEx.test(strTwo);//false
console.log(resultTwo);
```

In programming more generally (really DevOps), regular expressions
are frequently used to search log files.

### JSON
JSON (pronounced 'jay-sohn') stands for JavaScript Object Notation
and it's the string representation of an object (or other data type,
like an array). Objects exist in a computer's memory and can't be
transferred to another computer, but strings can!

JSON format is very popular (even ubiquitous) for web service calls
made by a web page. (HTTP) Calls made by a web page can send an object
as a string and receive another object as a string.

It's very easy for JavaScript to interact with JSON,
unlike other formats (especially including XML). JSON is also simple
to learn and easy to read, which makes it quite convenient for developing,
publishing, and using high-profile yet simpler web services.
(Web services are behind-the-scenes internet calls made by a browser
to get information ('what are the top Twitter postings?')
and to perform transactions ('send order to Amazon').)

#### JSON.stringify()

`JSON.stringify()` converts a JavaScript object to a string.
Here's an example.
```
var person = {"name": "Srini"};
console.log(person);//[object]
console.log(person.name);//Srini
var json = JSON.stringify(person);
console.log(json);//{"name":"Srini"}
console.log(json.length);//16, 'length' is a string function
```

#### JSON.parse()

`JSON.parse()` converts a string to a JavaScript object.
Here's an example. (If a string is encased in matching `"` characters,
the `"` character(s) within the string itself must `escaped`
with the `\` character to avoid confusion.)
```
var json = "{\"name\":\"Srini\"}";
console.log(json);//{"name":"Srini"}
console.log(json.length);//16, 'length' is a string function
var person = JSON.parse(json);
console.log(person);//[object]
console.log(person.name);//Srini
```

## Libraries
Libraries are collections of functionality (for JavaScript)
and styling (for CSS). For web pages, they reside outside of the source
code for the web page but are referenced by the web page.

Using libraries have one or more of the following benefits.

1) `Separation of Concerns` - It's common (and definitely recommended)
in software development to partition functionality by responsibility.
Just as a supermarket has different sections for different types of things,
A web page will separate out its core DOM, stylings, and JavaScript
into different files. It's imperative to do this on larger projects
to avoid confusion (the web page isn't a single huge mess).
2) `Better Quality` - Libraries are more focused which allows development
to be narrow and specialized. As defects are fixed and new features
are added, getting these improvements is just a matter of publishing
a new version of the library and the users of the library to select
this new version.
3) `Reuse` - A major advantage to using libraries is that common
functionality can be reused in different applications, which usually
saves time and a lot of money.
4) `External Knowledge` - Development, especially web development,
makes heavy use of popular libraries. This means that new members
of a team may already know and can use the libraries. And it also
means that existing team members can make more focused job postings
and ask better interview questions.

As of 2020, two popular JavaScript libraries are `jQuery` (for DOM
manipulation) and `Lodash` for advanced JavaScript processing.

Here's the jQuery way of getting a DOM element by its `id` attribute value.
Notice how jQuery uses considerably less code. jQuery can do much more
advanced things like get all DOM elements on a page that have a certain
CSS class (this could be useful for, for instance, making several 'div'
boxes disappear simultaneously when a user decides to cancel an action).
```
<html>
  <head>
    <script src="https://code.jquery.com/jquery-3.4.1.min.js" ></script>
    <script>
      //in jQuery, the '$' character represents the library
      //  the 'ready' function is a special (and cross-browser compatible)
      //  function that runs as soon as the web page is 'loaded enough'
      //  to allow DOM manipulation so that the user gets the finalized
      //  look of the web page as quickly as possible
      $(document).ready(function() {
        document.getElementById('traditional').value = 'Keep Tradition';
        $('#jquery').val('Try Something New');
      });
    </script>
  </head>
  <body>
    Traditional JavaScript - <input type="text" id="traditional" />
    <br />
    jQuery - <input type="text" id="jquery" />
  </body>
</html>
```

Here's the Lodash way of combining two JavaScript objects into one
with the fields of the first one taking precedence.
```
<html>
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/2.4.1/lodash.min.js" ></script>
    <script>
      var original = {"color": "red", "size": "large"};
      var override = {"color": "blue"};
      //in Lodash, the '_' character represents the library
      var result = _.defaults(override, original);
      //The resulting JSON object is - {"color":"blue","size":"large"}
      console.log("The resulting JSON object is - " + JSON.stringify(result));
    </script>
  </head>
</html>
```
### Frameworks

The goal of libraries is to help software developers get work done
sooner and better. Libraries like jQuery and Lodash _assist_ you
in getting work done. Think of them as tool kits
(like a hammer and a screwdriver).

Other libraries not only assist you but _tell_ you how the work should
be done. These are known as frameworks and include advanced web page
rendering frameworks like `React`, `Angular`, and `Vue`. They are less
like tool kits and more like assembly lines. Companies generally
expect web developers to know one of these frameworks as they
provide the capabilities and structure demanded by larger web apps.

### Obsolescence

Software development technologies, especially web technologies,
change very rapidly. Even cornerstone utility libraries like jQuery
are less necessary these days (as of 2020). There are many rendering
frameworks with passionate supporters but likewise something could
be seen as newer and cooler just a few years later. `Dojo` was seen
as up-and-coming about a decade ago but it hardly gets used now.

### Library Management
Tools like `node` can be used to gather libraries (specified in a
`package.json` file) used by an application. Combining this with
other tools like `Uglify` and `Webpack` produces a developer's setup
that can produce a single, high-optimized JavaScript file that's
ready for production.

Optimizations can include -
1) `Aggregation` - Every time the browser encounters a 'script' tag
that loads an external library, the browser completely stops processing
until the library is loaded. Loading one library instead of several
greatly reduces the time it takes for a page to render.
2) `Minification` - Reduce the size of a library by removing whitespace
and renaming variables to have smaller names, among other optimizations.
Smaller libraries load more quickly.
3) `Obfuscation` - Restructure the library's code so that it's harder
for people outside the organization to analyze (and potentially exploit).
4) `Streamline` - Remove unnecessary and unwanted code (like
`console.log()` statements) that shouldn't be used in Production code.

It all gets very complicated ....

### CSS Libraries
Like JavaScript, CSS can be loaded into a web page as an external
library. Companies frequently have a central web page styling
team develop common CSS definitions (among other reasons, to ensure
a consistent look and feel among the various pages of a corporate
web site, to provide a common brand). Individual development teams
then add and extend common stylings for a specific web page.

Like JavaScript, there are tools like `Less` and `Sass` that can
optimize the packaging of a CSS file.

Here's an example of loading CSS stylings. Make sure these files are
in the same directory.

Filename - 'styles.css'
```
h1
{
color: green;
border: '1pt solid black'
}

p
{
color: red;
background-color:#EFE7D6;
border: '1pt solid black'
}
```

Filename - 'testCss.html'
```
<html>
  <head>
    <link rel="stylesheet" type="text/css" href="styles.css"></link>
  </head>
  <body>
    <h1>This text should be green surrounded by a thin black box</h1>
    <p>This should be red text in a beige background
    all surrounded by a thin black box</p>
  </body>
</html>
```

### Bonus - Use 'Phaser' to Create a Game
Phaser is framework to make web app games. Examples and tutorials
of this framework can be found at https://phaser.io/ . Consider
studying this framework and making a game or a visual affect using
this framework (this may take several hours).
