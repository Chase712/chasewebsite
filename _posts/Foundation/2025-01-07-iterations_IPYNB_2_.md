---
comments: True
layout: post
title: Iteration Lesson No.1
description: An intro to Iterations
permalink: /csse/javascript/fundamentals/iteration/1
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

# Intro to iterations
- The basic gist of iterations are to repeat multiple actions for a desirable result
- Used to repeat code more efficiently compared to just writing out all the functions line by line

# For loops


```python
for (initialization; condition; increment) {
    // Code to execute
}
```

## Variable explanations
- Initialization - The starting point of the loop control variable, only excecuted once
- Condition - This is the function that is checked BEFORE each iteration of the loop. If the condition is true, then the code is executed. If the condition is false, then the execution is terminated
- Increment - The main updater of the loop variable when the iteration ends; excecuted at the end of each loop cycle

## Example


```python
for (let count = 0; count < 5; count++) {
    console.log(count);
}
```

## Parts explanation
- Initialization - (let count = 0) Here, the initalization of the code is shown as this is the starting value and only ran once
- Condition - (count < 5) Here, javascript determines whether the loop is true or false and determines when to terminate the code.
- Increment - (count++;) This is the main updater of the code, this increments the number by one each time. This part is also responsible for terminating the code when the counter reaches 5
- console.log(count) prints the output of the code

### Output

    0 

    1 

    2 

    3 

    4 

## Looping through an array


```python
%%js
const colors = ['red','blue','yellow','green','black'];

for (let i = 0; i < colors.length; i++){
    console.log(colors[i]); 
}
```

### Explanation
- const colors = ['red','blue','yellow','green','black']; acts as the array for the loop
- i++ scrolls through the array by one each time; ex: red to blue, blue to yellow, etc.
