---
comments: True
layout: post
title: Boolean Lesson 1
description: Booleans are a type of data that can represent only two possible values - true or false
courses: {'csse': {'week': 1}, 'csp': {'week': 1}, 'csa': {'week': 1}}
categories: ['Foundation']
sticky_rank: 1
---

# What are booleans? 

Booleans are a fundamental data type in programming that represent two possible values: true or false. 

They are commonly used to make decisions in code, control the flow of programs through conditional statements, and evaluate logical expressions. 

Booleans are essential for comparisons, determining equality, and managing program logic effectively. 


# Boolean commands 

== (Equal to): Checks if two values are equal in value but not necessarily in type (e.g., comparing numbers and strings with similar content like 5 == '5' evaluates to true).

!= (Not equal to): Checks if two values are different in value but not necessarily in type (e.g., 5 != '5' evaluates to false).

=== (Strict equal to): Checks if two values are equal in both value and type (e.g., 5 === '5' evaluates to false because one is a number and the other is a string).

!== (Strict not equal to): Checks if two values are different in either value or type (e.g., 5 !== '5' evaluates to true).

> (Greater than): Checks if the left value is larger than the right value (e.g., 10 > 5 evaluates to true).


>= (Greater than or equal to): Checks if the left value is larger than or equal to the right value (e.g., 18 >= 18 evaluates to true).

<= (Less than or equal to): Checks if the left value is smaller than or equal to the right value (e.g., 5 <= 10 evaluates to true).

# 1 - Basic Boolean Values

The basic boolean values are true and false, here is a quick example


```python
%%js

let isRaining = true;  // The condition "Is it raining?" is true.
let isSunny = false;   // The condition "Is it sunny?" is false.

console.log(isRaining);  // true
console.log(isSunny);    // false
```


    <IPython.core.display.Javascript object>


 
 isRaining is true, meaning the condition (it's raining) is correct.


 isSunny is false, meaning the condition (it's sunny) is false.

# 2 - Boolean Operators - And/Or/Not

# AND (&&) - Operator returns true if both conditions are true


```python
%%js
let isHot = true;
let isSummer = true;
let shouldGoToBeach = isHot && isSummer;  // Both conditions must be true

console.log(shouldGoToBeach);  // true

```


    <IPython.core.display.Javascript object>


# OR (||) - Operator returns true if at least one condition is true


```python
%%js 
let hasUmbrella = true;
let isRaining = false;
let canGoOutside = hasUmbrella || isRaining;  // Only one condition needs to be true

console.log(canGoOutside);  // true

```


    <IPython.core.display.Javascript object>


# NOT (!) - Changes the value of variable


```python
%%js
let isLoggedIn = false;
let isAdmin = !isLoggedIn;  // Inverts the value of isLoggedIn

console.log(isAdmin);  // true

```

# 3 - Boolean expressions

A Boolean expression evaluates to either true or false


```python
%%js
let userIsLoggedIn = true;
let isAdmin = true;

let Acessgranted = userIsLoggedIn && isAdmin;  // Both conditions must be true, we are using the And/&& operator here

console.log(Acessgranted);  // true

```


    <IPython.core.display.Javascript object>


The expression 'userIsLoggedIn && isAdmin' checks if the user is logged in and an admin. Since both conditions are true, acessgranted is true.
