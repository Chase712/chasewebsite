---
layout: post
title: Homework
description: Homework after condition lesson
categories: ['CSSE JavaScript Fundamentals']
courses: {'csse': {'week': 0}, 'csp': {'week': 0}, 'csa': {'week': 0}}
type: collab
permalink: /Conditions_HW
author: Yasna Ahmadi, Katherine Law, Yuna Lee, Namira Sharif
toc: True
---

## Homeworks  


### Part 1:
 Choose one from the three options to make a conditonal statement and if help is needed, use the Format at the bottom of the page.

#### Option 1: Grade Checker 
Example for the grade checker:

"F" if the grade is below 60.
"D" if the grade is between 60 and 69.
"C" if the grade is between 70 and 79.
"B" if the grade is between 80 and 89.
"A" if the grade is 90 or above.

#### Option 2: Weather app
Example for a weather app:

If the weather is sunny, print: "It's a great day to go outside!"
If the weather is rainy, print: "Don't forget your umbrella!"
If the weather is snowy, print: "Stay warm and safe!"

#### Option 3: Character Health Status
Example for a character health status:

If the health is 0, print: "Your character is dead."
If the health is between 1 and 25, print: "Critical condition! Find a health pack!"
If the health is between 26 and 75, print: "Your character is wounded. Be cautious."
If the health is above 75, print: "Your character is healthy and ready for action!"

### Part 2:
 Make another conditional statement with your idea.

 Make any If-Then, If, or Then-If statements with different ideas.


##### Format: 


```python
%%js

let yourVariable = ""; // Change this to your input or value

if (/* your first condition */) {
    console.log(/* your first output */);
} else if (/* your second condition */) {
    console.log(/* your second output */);
} else {
    console.log(/* your default output */);
}
```


    <IPython.core.display.Javascript object>



```python
%%js

let weather = "raining cats and dogs"; // Change this to your weather condition

if (weather === "sunny") {
    console.log("It's a great day to go outside!");
} else if (weather === "rainy") {
    console.log("Don't forget your umbrella!");
} else if (weather === "snowy") {
    console.log("Stay warm and safe!");
} else if (weather === "raining cats and dogs") {
    console.log("It's raining cats and dogs! Watch out for flying fur!");
} else {
    console.log("Weather is unpredictable today. Stay prepared!");
}

```


    <IPython.core.display.Javascript object>



```python
%%js
let animalLegs = 4; // Change this to the number of legs your animal has

if (animalLegs === 0) {
    console.log("This animal is likely a snake or a fish!");
} else if (animalLegs === 2) {
    console.log("This animal could be a bird or a human!");
} else if (animalLegs === 4) {
    console.log("This animal is probably a dog, cat, or lion!");
} else if (animalLegs === 6) {
    console.log("This animal might be an insect!");
} else {
    console.log("This is a very unique animal!");
}

```


    <IPython.core.display.Javascript object>


##### After testing any of the options, revise it and make another one from the options.

