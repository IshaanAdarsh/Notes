# JavaScript:
## In-file JS:
- Using Script Tags to implement Js in a HTML file
  - Unorganized and confusing (cluttered)
  - Code is not reusable

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Tutorial</title>
  </head>
  <body>
    <script type="text/javascript">
      // Comment Type1 (Single line)
      
      /* Multiple
      Line
      Comment*/
      
      document.write("Hello World")                     // Prints out Hello World on the WB
    </script>
  </body>
</html>
```

## Using External Files:
- Sript tag is used to point to the source of the Javascript
  - More organized ad you only have to change the code in the JS File
  - Reusable code

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Tutorial</title>
    <!-- Add the script tag to the head tag-->
    <script src = "index.js"></script>
  </head>
  <body>
    
  </body>
</html>
```
```js
      alert("The file is working")                    // Prints out an alert in the WB with the perticular message
```

## Writing HTML using JS:
- Use the document command to write valid HTML using JS.
- We can adjust where we want to place this HTML by changing the location of the script file
```js
document.write("<h1>Hello World!</h1>");
document.write("<hr>");
document.write("<p>This is a javascript tutorial</p>");
```
## Variables & Data Types:
- Variables are Containers for Storing Data.
- The five most basic types of data are strings, numbers, booleans, undefined, and null.
```js
var name = "Mike";                 // String w/ double quotes
var occupation = 'programmer';     // String w/ single quotes

var age = 20;                      // Integer
var gpa = 2.5;                     // Floating point number

var isTall;                        // boolean true/false
isTall = true;

var flaws = null;                  // This shows that the variable will not have any value
var description = undefined;       // This indicates that the variable doesn't have a value yet (but might in the future).

name = "John";                     // Easily change the value of the variable

document.write("Your name is " + name);
```
## Strings:
- A JavaScript string stores a series of characters
```js
var greeting = "Hello";
//   indexes:   01234

// Attribute -> length
// Method -> toUpperCase() [It requires a ()]
                                                                     // OUTPUT:
document.write( greeting.length + "<br>" );                          // The length of the String
document.write( greeting.charAt(0) + "<br>"  );                      // Character at index 0 = H
document.write( greeting.lastIndexOf("l") + "<br>"  );               // Last Index of the substring  = 3
document.write( greeting.indexOf("llo") + "<br>"  );                 // Index of the substring  = 2
document.write( greeting.indexOf("z") + "<br>"  );                   // Error = -1
document.write( greeting.toUpperCase());                             // Converts the string to upper case = HELLO
document.write( greeting.toLowerCase());                             // Converts the string to lower case = hello
document.write( greeting.substring(1, 3) + "<br>"  );                // Returns substring between the index - last index = el
document.write( greeting.endsWith("lo") + "<br>"  );                 // Returns boolean value = True
document.write( greeting.includes("he") + "<br>"  );                 // Checks if substring passed is preset = True
```

## Math & Numbers:
- Commands which deal with maths and numbers
```js
document.write( 2 * 3 + "<br>" );       // Basic Arithmetic: +, -, /, *
document.write( 2**3 + "<br>" );        // Exponents
document.write( 10 % 3 + "<br>" );      // Modulus Op. : returns remainder of 10/3
document.write( 1 + 2 * 3 + "<br>" );   // order of operations
document.write(10 / 3.0 + "<br><br>");  // int's and doubles


var num = 10;
num += 100;                              // +=, -=, /=, *=
document.write(num + "<br>");

num++;
document.write(num + "<br><br>");        // Incerements the number by one 

// Math class has useful math methods
document.write( Math.pow(2, 3) + "<br>" );      // 8
document.write( Math.sqrt(144) + "<br>" );      // 12
document.write( Math.round(2.7) + "<br>" );     // 3
document.write( Math.random() + "<br>" );       // Any number between 1 and 0 (decimal randoms)
```

## Getting User Input:
-  We use prompt to get the user to give input.
```js
var name = window.prompt("What is your name?");            //Generates a prompt box for the user to enter data
```
### Basic Calculator:
```js

var num1 = window.prompt("Num1: ");
var num2 = window.prompt("Num2: ");

num1 = parseFloat(num1);                          // Converts the string into float
num2 = parseFloat(num2);                          // Beacuse if we don't 2+3 = 23 (string concatenation) 

alert(num1 + num2);
```

## Array:
- JavaScript Array is a single variable that is used to store elements of different data types.
```js
var fruit = new Array("Apples", "Oranges");
var fruit = ["Apples", "Oranges"];
                  
document.write(fruit);                                    // Apples, Oranges
document.write(fruit[1]);                                 // Oranges
document.write(fruit.length)                              // 2
fruit[1] = Peaches                                        // Changes the value of Oranges to Peaches

// Splitting the string into an array
var fruit = "Apples, Oranges";
fruit = fruit.split(",")                                  // Splits it according to a specific element
document.write(fruit[0]);                                 // Apples
```

## Functions:
- Functions are the basic building block of JavaScript. Functions allow us to encapsulate a block of code and reuse it multiple times
```js
function addNumbers(num1, num2){
     return num1 + num2;
}

var sum = addNumbers(4, 60);
document.write(sum);
```
