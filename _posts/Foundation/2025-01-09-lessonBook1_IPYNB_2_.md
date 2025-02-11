---

---

---
layout: post
title: Variables Lesson 1
description: Introduction to JavaScript Variables
type: collab
comments: false
categories: [CSSE JavaScript Fundamentals]
permalink: /csse/lessons/variables/lessonBook1
---
# Introduction to Variables

Variables are labeled containers that store values, such as numbers or strings. They are defined by the programmer and can be accessed and, in most cases, changed throughout the code of the program. Some examples of variable usage are:
<ul>
    <li>
    Keeping scores in video games (Ex: score = 10)
    </li>
    <li>
    Storing user-inputted text (Ex: message = "Hello!")
    </li>
    <li>
    Keeping track of positions (Ex: playerX = 0)
    </li>
</ul>
Since many values need to change during a program runs, variables are extremely useful in all programming applications.

> Simplifying the yap: Variables are labeled containers that store values in code. They can be accessed and manipulated throughout the program and are extremely important in programming.


# Primitive Data Types

<h2>Numbers:</h2>
In many programming languages, numbers are broken down into two types: integers and floating-points. Integers are low-memory and refer to any whole number (Ex. 1, 14, or -57). Floating-point numbers take up more memory, but can store any number (Ex. 1.567, 8, 3.14159). <strong>In Javascript, all numbers are reffered to simple as "Number", meaning there is no difference between floats and integers.</strong>

<h3>Example</h3>


```python
%%js
let Score = 25; //Sets a variable called "Score" to 25
console.log(Score); //Prints the "Score" variable's value in the browser's console (will output "25")
Score += 10; //Increases Score by 10
```


    <IPython.core.display.Javascript object>



```python
%%js
let username = "pika43"; //Makes a string variable for the user's name
let friendName = 'TheNumber1Gamer'; //Makes another string variable for the user's friend's name
let score = 15; //Makes a number variable for the user's score

console.log(`The user ${username} has defeated ${friendName} and gained ${score} score.`); //Will output "The user pika43 has defeated TheNumber1Gamer and gained 15 score."
//The ${username} operator inserts the variable's value into the string and only works in strings using graves (`` instead of "" or '')
```


    <IPython.core.display.Javascript object>


<h2>Strings</h2>
    Strings are the primary method of storing non-number text in Javascript. <strong>Strings are marked with quotation marks at the beginning and end of the text</strong> (Ex. "This is a string!"). You can also use apostrophes (Ex. 'This is also a string!') or graves (Ex. `This string can be escaped!`)."
    <br>
    <br>
    Strings using quotations are the same as strings using apostrophes, and the type you use is usually up to personal preferences (there are some situations where you need apostrophes, but these are not very common). <strong>Strings can be combined using the "+" operator </strong>(Ex. console.log("This is a" + "string!") will output "This is a string!").
    <br>
    <br>
    <strong>Strings using graves can be escaped using the "${}" operator.</strong> This is useful when integrating other variables into strings (Ex. `Score: ${score}`).
    <br>
    <h3>Example</h3>

<h2>Booleans</h2>
Booleans are simple true or false values. They cannot store text or numbers and are only used as conditions. Booleans are either defined as variables (Ex. let online = true;) <strong>or outputted from comparisons using the "==", "<", ">", "<=", ">=", or "!" operators.</strong> Although they are very simple, booleans are a very important part of programming.
<br>
<h3>Example</h3>


```python
%%js
let number1 = Math.random(); //Sets "number1" to a number between 0 and 1
let number2 = Math.random(); //Sets "number2" to a different number between 0 and 1
let checkEquation = number1 < number2; //This will set the checkEquation variable to a boolean

console.log(checkEquation);

if(checkEquation){
    console.log("number1 is less than number2!");
}else{
    console.log("number2 is less than number1!");
}
```


    <IPython.core.display.Javascript object>


<h2>Objects</h2>
Objects are extremely useful data types. They take advantage of every other data type to create a collection of proprties that can be accessed and changed. Objects are great for organization and neat storage, as <strong>they minimize the need to create more variables.</strong>
<br><br>
When creating an object, use curly braces ({ and }) to start and end the object. Then, write the name of a property, add a colon (:) after, and then define it as a data type. Lastly, add a comma afterwards. You can repeat this to add more properties (Ex. {property1: "green", property2: "yellow"}).
<br>
<h3>Example</h3>


```python
%%js
let player = {name: "West", health: 100, canHeal: true}; //Creates an object called "player". The curly brackets ({}) indicate the start and end of the object definition.
console.log(player.name); //will output "West"
console.log(player.health); //will output "1000"
player.health = 50;
console.log(player.health); //will output "50"
```


    <IPython.core.display.Javascript object>


<h2>Symbols</h2>
Symbols are the newest addition to Javascript data types. They are completely unique, private pieces of data that are generally used when making properties of objects. They function similar to constant variables, as in they cannot change their value.
<br>
<h3>Example</h3>


```python
%%js
let newSymbol = Symbol("This is a symbol!"); //Creates a new symbol with a description of "This is a symbol!"
let object = { //Creates a new object
    [newSymbol]: 'Hello, World!', //Uses the symbol as a property of the object
};
console.log(object[newSymbol]); //Outputs "Hello, World!"
console.log(newSymbol.description); //Outputs "This is a symbol!"
```


    <IPython.core.display.Javascript object>



<h2>BigInt</h2>
<b1>
BigInt is another less commonly used data type. "BigInt" is short for (big integer), and they exist to stop the computer from having problems with numbers too big for the system.<br>
Computers can only hold a certain integer as the largest number (Ex. a 32 bit system has a largest Integer, 2,147,483,647. There is also a smallest number, -2,147,483,648). If the system detects a number larger than this, it will roll back to the smallest number and count up fron there. BigInts act as a failsafe for this type of problem. 
<br><br>
Define a BigInt with either an "n" at the end of a number, or a BigInt() function enclosing the number.
</b1>


```python
%%js
let veryBigNumber = 999999999999999999999999n; //The "n" at the end of the number marks this as a BigInt instead of a number.
console.log(veryBigNumber); //Outputs the BigInt
```


    <IPython.core.display.Javascript object>


<h2>Undefined</h2>
When a variable does not have an assigned value, it will show up as "undefined" whenever it is used. Intentional permanent usage of undefined values is not very common, as they tend to cause errors, and placeholder values are more common.
<br>
<h3>Example</h3>


```python
%%js
let password; //Declares a variable called "password" but does not assign it a value. Because no value was assigned, it automatically gets an undefined value.
console.log(password); //This will output "undefined" since "password" has no value.
password = 12345; //Gives "password" a value
console.log(password); //This will output "password"'s new value, "12345"
```


    <IPython.core.display.Javascript object>


<h2>Null</h2>
Null is like undefined's brother. The two are very similar, with the main difference being that null represents variables that do not exist at all while undefined represents the value of variables with no assigned value. Null is rarely used, but can be useful in specific cases. As an example, if you want to test if a variable has been defined earlier in your code, you may want to initially define the variable with a null value. Checking for a value later will allow you to see if it has properly been updated (or, if it stays null, it has not been updated).
<br>
<h3>Example</h3>


```python
%%js
let password = null;
console.log(password); //Password has not been updated yet
password = 12345;
console.log(password); //Prints updated password
```


    <IPython.core.display.Javascript object>


<h2>Summary</h2>
In this lesson, you have learned about the 8 main types of data that variables can store in JavaScript, while also seeing how a few other things work, like "if" statements, console.log(), and Math.random(). 
<ul>
    <li><strong>Numbers</strong> - Literally just numbers.</li>
    <li><strong>Strings</strong> - Data type for storing non-number text.</li>
    <li><strong>Booleans</strong> - Simple true/false values.</li>
    <li><strong>Objects</strong> - Collection of properties. Basically just variables in a variable.</li>
    <li><strong>Symbols</strong> - Unchangable unique identifiers.</li>
    <li><strong>BigInts</strong> - Data type for storing numbers too large for Javascript to handle </li>
    <li><strong>Undefined</strong> - Data type representing variables and properties without definitions. Basically just undefined variables</li>
    <li><strong>Null</strong> - Rare data type representing objects that do not exist.</li>
</ul>
<br>
