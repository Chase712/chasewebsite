---
comments: True
layout: post
title: Length of a List & Finding Minimum values, & Elements in an Array
description: A guide to finding the length of a list, minimum values, and elements in an array.
permalink: /_notebooks/project_lists/
categories: ['Lists']
author: Leila
---

## Length of a List
In JavaScript, the length of a list (also known as an array) refers to the number of elements it contains. It can be accessed using the (.length) property, which shows the total number of elements in the array.

## Javascript Example:

### Words Example:


```python
%%html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Display List</title>
</head>
<body>

    <h1>List of Cats</h1>

    <!-- This is where the list will be displayed -->
    <div id="cat-list"></div>

    <script>
        // The list that will display
        let my_list = ['cat0', 'cat1', 'cat2', 'cat3'];

        // Calculate the length of the list
        const length = my_list.length;

        document.getElementById('cat-list').innerHTML = `
            <p>List of cats: ${my_list.join(', ')}</p>
            <p>Length of the list: ${length}</p>
        `;
    </script>

</body>
</html>

```



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Display List</title>
</head>
<body>

    <h1>List of Cats</h1>

    <!-- This is where the list will be displayed -->
    <div id="cat-list"></div>

    <script>
        // The list that will display
        let my_list = ['cat0', 'cat1', 'cat2', 'cat3'];

        // Calculate the length of the list
        const length = my_list.length;

        document.getElementById('cat-list').innerHTML = `
            <p>List of cats: ${my_list.join(', ')}</p>
            <p>Length of the list: ${length}</p>
        `;
    </script>

</body>
</html>



### Number Example:


```python
%%js

let my_list = [2, 4, 6, 8, 10];//These are the #s that will be shown on the list
const length = my_list.length; //length will be 5
console.log(my_list);//This will show the given list 
```


    <IPython.core.display.Javascript object>


## Finding the Minimum Value:
You can use Math.min() to help you find the minimum value in an array.


```python
%%js
let numbers = [5, 8, 2, 1, 9];
let minValue = Math.min(...numbers);  // Spread operator to pass elements as arguments
console.log(minValue);  // Output: 1
```


    <IPython.core.display.Javascript object>


## Finding an Element in an Array:
To see if an element exists in an array you can use Array.prototype.includes()


```python
%%js 
let fishes = ['fish0', 'fish1', 'fish2'];
let hasfish0 = fishes.includes('fish0');  // Check if 'fish0' is in the array
console.log(hasfish0);  // Output: true
```


    <IPython.core.display.Javascript object>


## Popcorn Hack #3
Create a length of a list and print it in console.log()

1. Create a variable called "list" or "my_list_2"
2. Create a list of numbers or words in the brackets [] 
        Exp: let your_list = [3, 7, 9, 21];
3. Create a const length = your_list.length;
4. After all of that, finally print it out in console.log()
        Exp: console.log(your_list);


```python
%%js   

let " " = []; // create an variable 

const length = "".length; // create a const length

console.log(""); // print out your list in console

```


    <IPython.core.display.Javascript object>

