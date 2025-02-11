---
comments: True
layout: post
title: Iteration Lesson No.2
description: An intro to Iterations
permalink: /csse/javascript/fundamentals/iteration/2
categories: ['CSSE JavaScript Fundamentals']
author: Andrew Ge, Ishan Shrivastava, Pratheep Natarajan, and Ruhaan Bansal
---

# Intro to iterations

### The Break Statement

<li> We use it to terminate a loop/switch


### Output

0<br>

1<br>

2<br>

3<br>

4<br>

5<br>

When i = 6, the break statement is run, and it ends the loop early

## Continue Statement

used to restart a while or for loop

<li>when used,  ends the current iteration, and continues the next iteration

### Output

0<br>

1<br>

2<br>

3<br>

4<br>

5<br>

7<br>

8<br>

9<br>

Notice how it skips 6 and continues the loop


## For each loops

We did this in the previous lesson loop through an array

There is a different way to do this

These blocks of code both have the same output 

### Output

red <br>

blue <br>

yellow <br>

green <br>

black <br>


```python
%%js

for (let i = 0; i < 10; i++) {
  if (i == 6) {
    break;
  }
  console.log(i);
}

```


```python
%%js
const colors = ['red','blue','yellow','green','black'];

//color = i
for (let color of colors) { //checks each element in the list
    console.log(color); //prints each color
}
```


```python
%%js
const colors = ['red','blue','yellow','green','black'];

for (let i = 0; i < colors.length; i++){
    console.log(colors[i]); 
}
```
