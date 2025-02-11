---
layout: post
title: Variables Popcorn Hax Answer Key
description: Examples of correct answers for the Popcorn Hax Page.
type: collab
comments: False
categories: ['CSSE JavaScript Fundamentals']
permalink: /csse/lessons/variables/popcornHaxAnswerKey
---

<h1>Popcorn Hax Answer Key</h1>
- This file contains example answers for all the Hax. There are many right answers to every question, so don't panic if your answer does not exactly match ours. If it gets to the same endpoint, it's all good.

<h2>Exercise 1:</h2>


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


<h2>Exercise 2:</h2>


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


<h2>Exercise 3:</h2>


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



```python
%%js 
let gambling = Math.round(100 * Math.random()) 
let gamblingTalk = `Let's go gambling! CHK-CHK-CHK-${gambling}! Aww, dang it` //funny meme :3
console.log(gamblingTalk); //Prints result.
```


    <IPython.core.display.Javascript object>



```python
%%js
let m1 = "1"; //This is a string.
let m2 = 1; //This is a number.
console.log(m1 == m2);
//True due to loose being, well, loose (and only checking content).
console.log(m1 === m2);
//False due to strict equality checking for type as well as content.
```

<h2>Exercise 4:</h2>


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


<h2>Exercise 5</h2>


```python
%%js
// We will have several possible answers in the following cells. 
// If you kept the variable as message1, it makes sense to use a string. Otherwise, go nuts variable-wise.
let message1 = 16; 
console.log(message1);
console.log(typeof message1);
```


    <IPython.core.display.Javascript object>



```python
%%js
let message1 = "Hi Guys!";
console.log(message1);
console.log(typeof message1);
```


```python
%%js
let isTouchingGround = false;
console.log(isTouchingGround);
console.log(typeof isTouchingGround);
```

<h2>Exercise 6:</h2>


```python
%%js
let bigNumber = 9009009009009009009n
let x = Number.MAX_SAFE_INTEGER;
console.log(bigNumber > x); //Check to make sure your number is big enough. You're looking for a "true" output.
console.log(bigNumber);
```


    <IPython.core.display.Javascript object>


<h2>Exercise 7:</h2>


```python
%%js
let player = {
    name: "pika43", 
    health: 25,
    weapon = "Night's Edge"
    score = 10000000000 //Ten billion
    howManyIvy = 500
    isAlive = true
};

console.log(player.name);
console.log(player.weapon);

player.health = 1;
console.log(player.health); //Ouch
```

<h2>Exercise 8:</h2>


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


```python
//Bonus!
console.log("v THE POWER OF SYMBOLS v"); //THE POWER OF SYMBOLS

const enemy1Damage = 15;
const enemy2MaxHealth = 15;
console.log (enemy1Damage === enemy2MaxHealth);
//This will output true, since both variables are numbers with the same value. 
//With constants that are used for different reasons, this can be a problem. 
//You wouldn't subtract an enemy's max health from your to deal damage! What if you need these two to be unique?

const symbol1 = Symbol("Epic and Unique!");
const symbol2 = Symbol("Epic and Unique!");
console.log(symbol1 === symbol2);
//This, surprisingly, will output false. This is because each of these symbols are fully, entirely unique. 
//Even though both are symbol type variables with the same value stored inside them, the computer recognizes these both as unique items since they are different symbols.
```

<h2>Lesson 2, Exercise 1</h2>


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


<h2>Exercise dos<h2>


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


    <IPython.core.display.Javascript object>

