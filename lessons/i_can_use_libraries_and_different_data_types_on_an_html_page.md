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

#### String

#### Date

#### Undefined and Null

#### Array

#### Object

#### Function

### JSON

#### JSON.stringify()

#### JSON.parse()

https://phaser.io/examples/v3/view/display/tint/tint-fill-effect