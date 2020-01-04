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

#### Function

#### Regular Expressions

### JSON

#### JSON.stringify()

#### JSON.parse()

https://phaser.io/examples/v3/view/display/tint/tint-fill-effect