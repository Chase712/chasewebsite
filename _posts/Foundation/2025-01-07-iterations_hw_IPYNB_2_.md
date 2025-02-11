---
comments: True
layout: post
title: Iteration Homework
description: Iterations HW
permalink: /csse/javascript/fundamentals/iteration/hw
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

### Exercise 1: Multiplication Table
##### Write a JavaScript program to print the multiplication table for a given number.



##### Example:
##### Input: 3
##### Output:
##### 3 x 1 = 3
##### 3 x 2 = 6
##### ...
##### 3 x 10 = 30


```python
let number = 3; // You can change this number
for (let i = 1; i <= 10; i++) {
  console.log(`${number} x ${i} = ${number * i}`);
}
```

### Exercise 2: Nested Loops
##### Write a JavaScript program using nested loops to generate the following pattern:

##### Output:
##### 0
##### 00
##### 000
##### 0000
##### 00000


```python
for (let i = 1; i <= 5; i++) {
  console.log('0'.repeat(i));
}
```

### Challenge Exercise: Prime Numbers
##### Write a JavaScript program to print all prime numbers between 1 and 50.


```python
for (let num = 2; num <= 50; num++) {
  let isPrime = true;
  for (let i = 2; i < num; i++) {
    if (num % i === 0) {
      isPrime = false;
      break;
    }
  }
  if (isPrime) {
    console.log(num);
  }
}
```

# End of Homework
