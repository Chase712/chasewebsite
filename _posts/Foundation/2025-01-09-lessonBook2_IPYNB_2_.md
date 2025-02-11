---
layout: post
title: Variables Lesson 2
description: Now that you know the types of variables, let's see how they can be used in different real-world contexts.
type: collab
comments: False
categories: ['CSSE JavaScript Fundamentals']
permalink: /csse/lessons/variables/lessonBook2
---

Plan:
calculations with variables
advanced declarations


Advanced Application of Variables 
(Normal people talk: Common Uses)

<h2>How Can We Use Variables?</h2>
<b1>
Variables are useful in virtually every context. Do you want to store a dynamically changing value, like score or health? Use a variable. Want to contain messages that can contain changing pieces of information? Variables. Want to intentionally have empty values for later use (for whatever reason)? Variables.
</b1>

<b1>Score is a great example on how to use variables in an actual context. In this example, every time the program is run, the Score variable increments by 1.</b1>


```python
%%js
// Get the current score from localStorage, or set it to 0 if it doesn't exist
let score = parseInt(localStorage.getItem("score")) || 0;

// Increment the score
score += 1;

// Save the updated score back to localStorage
localStorage.setItem("score", score);

// Log the current score
console.log(`Your score is now: ${score}`);
```


    <IPython.core.display.Javascript object>


Now, lets see variables being used in a a full "game"


```python
%%js

let spaceship = "Mort's Flying Monkey";
let initialFuel = 100; 
let distanceTraveled = 0; 
let fuelConsumptionRate = 2; 

let selectedFuel = 50; 
let missionStatus = ""; 
let fuelDrops = Math.floor(Math.random() * 3) + 1; 


function collectFuel(currentFuel, distance) {
  let fuelCollected = Math.floor(Math.random() * 20) + 10; 
  console.log(`At distance ${distance}, a fuel drop was found! Collected ${fuelCollected} fuel.`);
  return currentFuel + fuelCollected;
}

if (selectedFuel > initialFuel) {
  missionStatus = "Mission failed. Not enough fuel!";
} else if (selectedFuel <= 0) {
  missionStatus = "Mission aborted. Fuel must be greater than zero.";
} else {

  for (let i = 0; i < fuelDrops; i++) {
   
    distanceTraveled += selectedFuel / fuelConsumptionRate;
    initialFuel -= selectedFuel;

    
    if (initialFuel <= 0) {
      missionStatus = `Mission failed! The spaceship ran out of fuel after traveling ${distanceTraveled} units.`;
      break;
    }

    
    initialFuel = collectFuel(initialFuel, distanceTraveled);
  }

  
  if (initialFuel > 0) {
    missionStatus = `Mission successful! The spaceship ${spaceship} traveled ${distanceTraveled} units of distance. Remaining fuel: ${initialFuel}`;
  }
}

console.log(`Spaceship: ${spaceship}`);
console.log(`Fuel given: ${selectedFuel}`);
console.log(`Distance traveled: ${distanceTraveled}`);
console.log(`Remaining fuel: ${initialFuel}`);
console.log(`Mission Status: ${missionStatus}`);
// hi down here... yes we know this doesnt use any of the cool variable types we talked about last lesson sorry not sorry
```


    <IPython.core.display.Javascript object>



```python
function collectFuel(currentFuel, distance) {
    let fuelCollected = Math.floor(Math.random() * 20) + 10; 
    console.log(`At distance ${distance}, a fuel drop was found! Collected ${fuelCollected} fuel.`);
    return currentFuel + fuelCollected;
  }
```

- In this first bit of the code, a function is created to add a random amount of fuel to the fuelCollected variable that was previously defined


```python
if (selectedFuel > initialFuel) {
    missionStatus = "Mission failed. Not enough fuel!";
  } else if (selectedFuel <= 0) {
    missionStatus = "Mission aborted. Fuel must be greater than zero.";
  } else {
    // Proceed to the mission loop
  }
```

- In this part of the code, the values inside variables are being compared. Trying to do this without variables would be very, very, very, very, extremely, extremely annoying and maybe even not possible

### Object Oriented Variable Usage

You now know how to define variables and vaguely know how to use them. However, with OOP programming there are two more variable types. (for now?)

><h2>Static Variable</h2>

Static variables are variables that are "static" throughout all instances of the class. They can also be accessed directly in the class without having to make a instance.


```python
%%js 
class myCharacter {
    static Health = 100; //this is the static variable

    
    
}
console.log(myCharacter.Health)
```


    <IPython.core.display.Javascript object>


In this example, the static variable, noted by the "static" keyword, defines Health for the class "Mycharacter." If I were to make another character under the class Mycharacter, this health value would become a shared health pool - if one character takes damage the other's health is affected as well.

Now, lets see if this static variable works in practice.


```python
%%js
class Dog {
    static Health = 100
    constructor(name, age) {
        this.name = name // I wonder what kind of variable this is
        this.age = age
    }
}

let myDog = new Dog("QuadraticFormula", 2)
console.log(myDog.name)
console.log(Dog.Health) //since this variable is shared across all instances, to access this dog's health you access from the class.

//to show that this is truly shared across all classes, lets modify the health then make another dog.

Dog.Health = 75

let otherDog = new Dog("woke up on both sides of the bed", 10)
console.log(otherDog.name)
console.log(Dog.Health) //accessing this dog's health
```


    <IPython.core.display.Javascript object>


Other common use cases for Static Variables are counters, configuration settings, global constants, and could even be used to store base stats for characters in a video game

><h2>Instanced Variables</h2>


Now, you may have seen another kind of variable in my example above. What is this? you might ask. Well, as the tile suggests, this is an instanced variable.

As the name suggests, an instanced variable can be set differently for any instance of a class.


```python
%%js
class Character {
    constructor(health){
    this.health = health;
    }

}
globalThis.dumbmist = new Character(5);
dumbmist.health = 2; //damaging devon 
console.log(dumbmist.health);
```


    <IPython.core.display.Javascript object>


So in this example, health as a whole defines the health of the character (yeah who woulda guessed). "this.health" however creates an instance of this health variable for every character that is under this class. These instanced variables are only accessible in the object and changing one instance does not affect any others.


```python
%%js
// just so you guys can see that Im not lying
class Character {
    constructor(health) {
    this.health = health;
    }

}
globalThis.dumbmist = new Character(5);
globalThis.evansvetina = new Character(7);
globalThis.weststefany = new Character(9);

dumbmist.health = 2; //damaging devon
evansvetina.health = 1; //damaging evan
weststefani.health = 3; //damaging west
console.log(dumbmist.health);
console.log(evansvetina.health);
console.log(weststefany.health);
```


    <IPython.core.display.Javascript object>

