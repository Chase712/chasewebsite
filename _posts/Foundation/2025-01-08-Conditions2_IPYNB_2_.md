---
layout: post
title: Conditions-2
description: Condition Lesson 2
categories: ['CSSE JavaScript Fundamentals']
permalink: /csse/javascript/fundamentals/Conditions2
author: Yasna Ahmadi, Katherine Law, Yuna Lee, Namira Sharif
toc: True
comments: True
---

# All About Conditions

## Faster ways ;)

<b>Switch Statements</b>
Switch Statements are much faster and effecient then writing a bunch of If Else Statements. A switch statement helps your program make choices based on a value. It checks the values with different cases, like options, and then runs the code for the matching case. If the value is unknown it runs the default option. 

<b>Benefits of Using Switch Statements</b>
    - Readability: Easier to read and maintain when handling many possible values.
    - Efficiency: Faster in some languages, as the implementation often uses a jump table or other optimization
    - Structured Approach: Clearly separates conditions into cases.
- For Example: If Color is Blue, it prints the color Blue. If Color is Pink, it prints the color Pink. If it is neither, it prints I dont know. 

Example in Code:


```python
%%js
let color = "Yellow";
switch (color) {
    case "Blue":
        console.log("The color is Blue.");
        break; // Stops further checks once this case runs
    case "Pink":
        console.log("The color is Pink.");
        break;
    default:
        console.log("I don't know the color.");
}

```


    <IPython.core.display.Javascript object>




<b>How It Works<b/>

- The switch keyword is followed by the variable (color) to evaluate.
- The program checks each case to find a match.
- When a match is found, it executes the code under that case.
- The break statement prevents the program from continuing to the next cases unnecessarily.
- If no cases match, the default block runs.

<b>More Real Life Examples in Javascript<b/>


```python
%%js
let grade = 85;
if (grade >= 90) {
    console.log("You got a A!");
} else if (grade >=80) {
    console.log("You got a B!");
} else if (grade <=80) {
    console.log("You need to work harder!");
}
```


    <IPython.core.display.Javascript object>

