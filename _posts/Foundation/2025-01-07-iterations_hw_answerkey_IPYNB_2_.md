---
comments: True
layout: post
title: Iteration Homework Answer Key
description: Iterations Homework Answer Key
permalink: /csse/javascript/fundamentals/iteration/Homework_Answerkey
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

```python
%%js
function multiplicationTable(number) {
    for (let i = 1; i <= 10; i++) {
        console.log(`${number} x ${i} = ${number * i}`);
    }
}
multiplicationTable(3);
```


    <IPython.core.display.Javascript object>



```python
%%js 
for (let i = 1; i <= 5; i++) {
    let zeroes = "";
    for (let j = 1; j <= i; j++) {
        zeroes += "0";
    }
    console.log(zeroes);
}
```


    <IPython.core.display.Javascript object>



```python
%%js 
function isPrime(num) {
    if (num <= 1) return false;
    for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) return false;
    }
    return true;
}

for (let i = 1; i <= 50; i++) {
    if (isPrime(i)) {
        console.log(i);
    }
}
```


    <IPython.core.display.Javascript object>

