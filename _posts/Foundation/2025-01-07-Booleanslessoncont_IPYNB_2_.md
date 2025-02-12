---
layout: post
title: Boolean Lesson 2
description: Booleans continued
categories: ['Foundation']
courses: {'csse': {'week': 2}, 'csp': {'week': 1}, 'csa': {'week': 1}}
permalink: /CSSE/Javascript/Booleans2/p3
comments: True
sticky_rank: 1
---

<style>
p {
    color: darkblue;
    font-family: 'Courier New';
    font-size: 18px;
}

h3 {
    color: darkblue;
    font-family: 'Courier New';
}
</style>

<body>

<p> Booleans are just true and false statements. If you put " 3 > 1", the output would be true, because 3 is more than 1 (wow so amazing). </p>
 
 <br>

<h3>Booleans Example</h3>
<p> Below is an example of what a boolean is. This is how they work. Running the cell will check if the variables are true or false. Based on the variables, the boolean will output either true or false, which you can use to do certain commands/actions. </p>

 </body>


```python
%%js

//Play around with the variables to see what happens
let keyInserted = true;
let correctKey = false;
let lockPick = false;

if (lockPick) {
    console.log("Door opened.")
}
else {
    //Check if the key you have was inserted and is the correct key
    if (keyInserted){
        console.log("Inserted key into door.")
    }
    else {
        console.log("Insert key into door.")
    }
    if (keyInserted && correctKey){
        console.log("Door opened.")
    }
    else {
        console.log("Incorrect key, door did not open.")
    }
}


```


    <IPython.core.display.Javascript object>


<style>
p {
    color: darkblue;
    font-family: 'Courier New';
    font-size: 18px;
}

h3 {
    color: darkblue;
    font-family: 'Courier New';
}
</style>

<body>
<h3>More information on Booleans</h3>
<p> The Boolean() command lets variables that are not booleans to become booleans.<br>
<br>
<p> The Boolean() command follows these following rules: </p>
    <br>
    <ol>
    <li> True - if there is an interger inside Boolean(), that is not 0. </li>
    <li> False - if there is an interger inside Boolean(), that is 0.</li>
    <li>True - if the variable inside Boolean() is a string, and has something in it.</li>
    <li>False - if the variable inside Boolean() is a string, and does not have something inside it. </li>
    </ol>
    
</body>


```python
%%js 

let l = "qrstuv";
let m = 48;
let n = "wxy and z"
let o = 0;
let p = 1245;

if (Boolean(l) == true ) {
    console.log("A: Correct!");
} else {
    console.log("A: Incorrect!");
}
if (Boolean(m) == true ) {
    console.log("B: Correct!");
} else {
    console.log("B: Incorrect!");
}
if (Boolean(n) == true) {
    console.log("C: Correct!");
} else {
    console.log("C: Incorrect!");
}
if (Boolean(o) == true) {
    console.log("D: Correct!")
} else {
    console.log("D: Incorrect!");
}
if (Boolean(p) == true) {
    console.log("E: Correct!");
} else {
    console.log("E: Incorrect!");
}
if (Boolean(l) == true && Boolean(m) == true) {
    console.log("Yay! It's the ABC's!");
} else {
    console.log("Where's the rest?");
}
```
