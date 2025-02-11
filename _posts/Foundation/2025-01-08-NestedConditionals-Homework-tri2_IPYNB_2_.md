---
layout: post
title: Nested Conditionals, Homework
description: Homework for nested conditionals
type: issues
comments: True
---

### Homework Objectives

You and your friend want to do different things at the amusement park. To decide, you do a coin flip. Heads means that you get to choose where to go and tails means that your friend gets to choose. If you go on a ride, be sure to check if you are the right height and have enough tickets, and if you go to a food stand, make sure that you have enough money and that the food is in stock. Be creative, and make sure to use nested conditionals!

### Instructions

1) Create a JavaScript file (Ex. insertName.js)

2) Plan out what you will be doing and make variables for the necessary things. There will be a coin flip, so make a variable for that. If there are rides, make a value for the amount of tickets the person has and what height they are. If they go to a food stand, you can make a variable for the amount of money that you have and if the food is in stock.

3) Use Math.random() for the coin flip. This generates a number between 0 and 1, so then you multiply this value by 2 and put it inside Math.floor() to round down and get either 0 or 1. Make this the coin flip variable.

4) Use an if statement to check what the result of the coin flip was and use console.log to print out a statement to see who won or lost the coin flip. Along with that, print out where they are going next.

5) Use more if statements inside of if statements to check if the person can do what they want to do. (Are they tall enough, do they have enough money, etc.)

6) After all the checks, print out a result of what happened. If you get stuck, you can look at the examples in the popcorn hacks. Please don't copy and paste, though! 



```python
// Step 1: Coin flip to decide who chooses
let coinFlip = Math.floor(Math.random() * 2); // Generates 0 or 1

// Step 2: Declare necessary variables for rides and food stands
let ticketsAvailable = 5; // Number of tickets you have
let height = 150; // Your height in cm
let moneyAvailable = 10; // Amount of money you have
let foodInStock = true; // If the food is in stock

// Step 3: Coin flip outcome and decision making
if (coinFlip === 0) {
    console.log("We go to the rides!");

    // Check for rides
    if (height >= 140 && ticketsAvailable >= 3) {
        console.log("You're tall enough and have enough tickets for the ride!");
    } else {
        console.log("You can't go on the ride.");
    }
} else {
    console.log("Your friend gets to choose where to go!");

    // Check for food stand
    if (moneyAvailable >= 5 && foodInStock) {
        console.log("You can buy food, and it's in stock!");
    } else {
        console.log("Either you don't have enough money or the food isn't in stock.");
    }
}

```
