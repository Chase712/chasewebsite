---
layout: post
title: Variables Popcorn Hax
description: Exercises to do mid-lesson, when instructed. Designed to be fairly easy and help you apply a basic understanding of variables you should already have from the lesson.
type: collab
comments: False
categories: ['CSSE JavaScript Fundamentals']
permalink: /csse/lessons/variables/popcornHax
---

<h1>Popcorn Hax</h1>

To access printed results using console.log, follow this simple set of steps.
1: Access the "Help" button near the top of your screen (next to to "Terminal" and "Window). It looks something like this on macOS:<br>
<img width="844" alt="image" src="https://github.com/user-attachments/assets/18465a9b-e7e3-4f9d-8653-3ede47e2dfc6" />
<br>
After clicking help, the drop-down menu should have a "Toggle Developer Tools" option. Click it, and navigate to the console menu.
Then, look for a little O with a line through it. Click this to clear the console.

<h2>Lesson 1, Exercise 1:</h2><br>
Define a variable "charHealth" as an integer value of 100. Then, run a command to print the value and type of charHealth.



```python
%%js
//On this line, define charHealth.
let charHealth = 100.0;
//Run the command to print charHealth's value here.
console.log(charHealth);
//Expected output: 100.0

//Run the command to check the type of variable here.
console.log(typeof charHealth);
//Expected output: number
```


    <IPython.core.display.Javascript object>


<h2>Exercise 2:</h2><br>
Define two variables: "charHealth" and "damage". Then, combine the two to update charHealth. Make sure they are the same type of variable - otherwise, you will not be able to combine them.


```python
%%js
//Define variables up here. Make sure they are both numbers.
let charHealth = 100.0;
const damage = 13.5;

//Note: const used for damage here for no particular reason other than some basic logic: health is a dynamically changing variable, 
//but this source of damage is just there as a constant, meant to change health by a certain amount.

//Update charHealth after the player has taken damage. The character should lose health relative to damage taken. Print your results.
charHealth -= damage;
console.log(charHealth);
//Expected output: 86.5
```


    <IPython.core.display.Javascript object>


<h2>Exercise 3:</h2><br>
Create two parts of a message, and store each part as a separate variable. Combine these variables into a new one, finalMessage, and print its results.


```python
%%js
//Define variables and combine them here
let messagePart1 = "Hello, ";
let messagePart2 = "world!"
let finalMessage = messagePart1 + messagePart2;
//Print results here.
console.log(finalMessage);
//Expected output: Hello, world!
```


    <IPython.core.display.Javascript object>


<b1>
Make sure to end each line with a semicolon (;). 
<br>Part 2: Using this if conditional, see if you can get the console to output "You have successfully manipulated these strings! Good Job!" If you don't get the desired result, try again.
</b1>


```python
%%js
let m1 = "Hello, ";
let m2 = "world!"; 
if (m1 + m2 === "Hello, world!"){
    console.log("You have successfully manipulated these strings! Good Job!");
} else {
    console.log("Failed to match strings. Try again.");
}
console.log(m1 + m2);

//Alternatively, you could have made m1 and m2 something like this:
m1 = "Hello, world";
m2 = "!";  
if (m1 + m2 === "Hello, world!"){
    console.log("You have successfully manipulated these strings! Good Job!");
} else {
    console.log("Failed to match strings. Try again.");
}

console.log(m1 + m2); //Still outputs the same thing as the old version. As long as the combined version is "Hello, world!" this will work.
```


    <IPython.core.display.Javascript object>


Try defining a score variable and a string that displays the player's score. A very basic version of this has been set up for you here, using Math.random() to get a random number.


```python
%%js 
let gambling = Math.round(100 * Math.random()) 
let gamblingTalk = `Let's go gambling! CHK-CHK-CHK-${gambling}! Aww, dang it` //funny meme :3
console.log(gamblingTalk); //Prints result.
```


    <IPython.core.display.Javascript object>


Lastly, here's a quick way to learn the difference between =, ==, and ===.


```python
%%js
let m1 = "1"; //This is a string.
let m2 = 1; //This is a number.
console.log(m1 == m2);
//True due to loose being, well, loose (and only checking content).
console.log(m1 === m2);
//False due to strict equality checking for type as well as content.
```


    <IPython.core.display.Javascript object>


<h2>Exercise 4:</h2><br>
Here, a Math.random function creates a number from 0 to 1. Using the conditional set up for you and your knowledge of booleans, create a system that checks if the number created is greater than 0.7.


```python
%%js
let isGreaterThan = false; //By default, this is false. That means if the program doesn't change it, 
                           //it will stay false and output false (which is what we want).
let randomNum = Math.random(); //Random number
if (randomNum > 0.7) { 
    isGreaterThan = true;
} 
console.log(isGreaterThan); //Outputs the value of isGreaterThan

//Should get true and false values (though more false than true).

```


    <IPython.core.display.Javascript object>


<h2>Exercise 5:</h2><br>
- Fix this code to correctly output the type of data message1 is.
- In code, undefined and null are not used intentionally very often. This exercise is an example on why it is useful: since message1 is not defined, you can check this with console.log(). If this results in an undefined output, you can go change the variable to be correctly defined.


```python
%%js
// We will have several possible answers in the following cells. 
// If you kept the variable as message1, it makes sense to use a string. Otherwise, go nuts variable-wise.
let message1 = 16; 
console.log(message1);
console.log(typeof message1);
```


    <IPython.core.display.Javascript object>


<h2>Exercise 6:</h2><br>
Create a bigInt with a value of your choosing. Check to make sure it's a big enough number. The highest number in JS is 9007199254740990, and can be referenced with the property Number.MAX_SAFE_INTEGER.


```python
%%js
let bigNumber = 9009009009009009009n
let x = Number.MAX_SAFE_INTEGER;
console.log(bigNumber > x); //Check to make sure your number is big enough. You're looking for a "true" output.
console.log(bigNumber);
```


    <IPython.core.display.Javascript object>


<h2>Exercise 7:</h2><br>
- Create a "player" object with as many properties as you can think of. A minimum of 5 properties and at least 3 different types of variables must be used to complete this exercise.
- After this, print 2 of those variables. One has already been done for you, and the other started. Lastly, change the player's health and print it again.


```python
%%js
let player ; {
    name: "pika43", 
    health: 25,
    weapon ; "Night's Edge"
    score = 10000000000 //Ten billion
    howManyIvy ; 500
    isAlive ; true
};

console.log(player.name);
console.log(player.weapon);

player.health ; 1;
console.log(player.health); //Ouch
```


    <IPython.core.display.Javascript object>


<h2>Exercise 8:</h2><br>
Create a "user" object with a password variable as a symbol. Other than that, customize the object similarly to the previous exercise (Minimum of 5 variables, minimum of 3 types). There's a nifty little bonus at the bottom of this exercise which shows the power of symbols.


```python
%%js 
const password = Symbol();
const backupPassword = Symbol();
let user ={
    [password]: "IL0V3C0DING"
    [backupPassword]:  "IL0V3C0DING"
    username: "pika43" //Fill in the rest of the object's properties. Replace this username with your own.

}
//Referencing symbols looks like this:
console.log(user[password]);
//This outputs the value of "password" you assigned earlier.

```


    <IPython.core.display.Javascript object>


<h2>Lesson 2, Exercise 1:</h2>
<b1>
btw, classes are thing that you will learn later. I'm not explaining them now jus roll with it
</b1>

Imagine this: you have a brand-spankin' shiny new game that you made, and you want to keep track of how many players you have. Using context clues and my helpful comments, fill in the blanks.

Next, try and see if you can make the player number increase.


```python
%%js 
class Player {
    static totalPlayers = 0 //hmm I wonder if this blank might have anything to do with line 4 after the .

    constructor(name) {
        this.name = name // i wonder what name could be
        this.id = ++Player.totalPlayers
    }

    static getTotalPlayers() { // this is the thing that will give you the number of players. remember to put a Player. in front
        return Player.totalPlayers
    }
}
const player1 = new Player("RedIsSus")
const player2 = new Player("Jimmy")
// I wonder if making new players would increase the player count

console.log(Player.getTotalPlayers()) // you want to print the *function* that will give you the player numbers
```


    <IPython.core.display.Javascript object>


<h2>Exercise Dos</h2>


```python
%%js
class Car {
    constructor(color, model) {
        this.color = color;    // Instance variable
        this.model = model;
    }
}

const car1 = new Car("Red ", "2006 Nissan Murano");
const car2 = new Car("Blue ", "2019 Toyota Corolla");

console.log(car1.color + car1.model);  // Prints car colors and models.
console.log(car2.color + car2.model);  

car1.color = "Yellow ";    // Only changes car1.
console.log(car1.color + car1.model);  // Logs changes.
console.log(car2.color + car2.model);  // No change from earlier.
```
