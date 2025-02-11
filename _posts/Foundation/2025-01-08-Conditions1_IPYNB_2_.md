---
layout: post
title: Conditions-1
description: Condition Lesson 1
categories: ['CSSE JavaScript Fundamentals']
permalink: /csse/javascript/fundamentals/Conditions1
author: Katherine Law, Yasna Ahmadi, Yuna Lee, Namira Sharif
toc: True
comments: True
---

# All About Conditions

## ***What is conditions?*** 
Conditional Statements are what happens next in the program when a certain condition is met. 
=======
### **Key Components**
Condition: A question the computer evaluates, such as "is this true or false?"

Action: Checks if something is true or false

Optional Action: Runs different parts of the code depending on that

### **Conditional Statements**: 
There are many types of statements that all help do different things depending on the amount of values, answers and etc..

<u>If Statements</u>: Checks if a condition is true and then executes something. 
- For example: If it's raining, take an umbrella

<u>Branch Statements</u>: Provides multiple options depending on the condition.
- For example: If it's raining, take an umbrella, if not wear sunglasses.

<u>If Else Statements</u>: Checks if a condition is true or false and then provides an execution for both. "If" checks if something is true. "Else" checks if something is false.
- For example: If you bought a membership the program will print "Welcome in."
If you didn't buy a membership the program will print "Invalid Membership"

<u>Else If Statements</u>: Checks Multiple conditions first if they are true and if not does the final condition
- For Example: If you are younger then 10: You get a popsicle
If you are you 10 or older but not older then 20: You get a sandwhich
If you are older or 20: 






### **Breaking it Down** 
Example in Javascript:


```python
%%js

if (5>3) {
    console.log("5 is greater than 3.");
} 

```


    <IPython.core.display.Javascript object>


Adding else when using conditions in Javascript:


```python
%%js
let age = 18;
if (age>= 18) {
    console.log("You can vote.");
} else if (age<= 18) {
    console.log("You cannot vote yet.");
}
```


    <IPython.core.display.Javascript object>

