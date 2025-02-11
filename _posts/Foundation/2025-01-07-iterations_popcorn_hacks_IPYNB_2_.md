---
comments: True
layout: post
title: Iteration Popcorn Hacks
description: Iterations Popcorn Hacks
permalink: /csse/javascript/fundamentals/iteration/Popcorn_Hacks
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

# Popcorn Hacks on Iterations in JavaScript

##### Instructions:
##### Complete the exercises below in JavaScript.
##### You can run and test your code in a JavaScript environment.

### Exercise 1: Counting with a For Loop
##### Write a JavaScript for loop that prints all numbers from 1 to 10.

##### Example:
##### Output:
##### 1
##### 2
##### 3
##### ...
##### 9 
##### 10 

### Exercise 2: Sum of Numbers
##### Write a function in JavaScript to calculate the sum of all numbers from 1 to n using a loop.

##### Example:
##### Input: 5
##### Output: 15 (because 1 + 2 + 3 + 4 + 5 = 15)


### Exercise 3: Looping through Arrays
##### Write a JavaScript program to iterate through an array of names and print each name.


```javascript
%%javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);
}
```


    <IPython.core.display.Javascript object>



```python
%%js
const colors = ['red','blue','yellow','green','black'];

for (let i = 0; i < colors.length; i++){
    console.log(colors[i]); 
}
```


    <IPython.core.display.Javascript object>



```python
%%js 
function sumNumbers(n) {
    let sum = 0;
    for (let i = 1; i <= n; i++) {
        sum += i;
    }
    return sum;
}
console.log(sumNumbers(5)); // Output should be 15
```


    <IPython.core.display.Javascript object>



```python
%%js 
const names = ["Jack", "Chase", "Hope", "Nico"];
for (let i = 0; i < names.length; i++) {
    console.log(names[i]);
}
```


    <IPython.core.display.Javascript object>

