---
layout: post
title: Accessing, Deleting, and Assigning a Value to Elements
description: How to access elements in a list, and applying that to delete, add, and alter elements in a list.
categories: ['JavaScript']
author: Zoe Chow
comments: True
---

# Accessing and Deleting Elements

## Accessing an Element

In javascript, we use a system of positive indexing to access elements. With postive indexing, elements are referred based on their position in reference to the start of the list. Counting starts at 0, so the first item in list would be position 0.

Ex: let list = [1, 2, 3, 4, 5];

So in this case to reference 1 you would write list[0] and not list[1]. list 1[1] would refer to 2.









```python
%%js

let list = [1, 2, 3, 4, 5];

console.log(list[0]); // prints 1
console.log(list[1]); // prints 2
console.log(list[2]); // prints 3
console.log(list[3]); // prints 4
console.log(list[4]); // prints 5 

```


    <IPython.core.display.Javascript object>


## Deleting an Element

To delete an element in javascript, you would use pop(index) or splice(). 

pop(index) - removes/deletes the last element in a list

splice(position(index), # of elements your deleting) - deletes an element or elements from a specific position in the list.


```python
%%js

let list = ['One', 'Two', 'Three', 'Four', 'Five'];

// original list
console.log(list)

// deletes the last value
list.pop();
console.log(list)

// deletes the third value, Three
list.splice(2, 1);

console.log(list)

```


    <IPython.core.display.Javascript object>


Example of deleting multiple elements with splice in HTML


```python
%%html
<!-- HTML output -->
<div id="listContainer"></div>

<script>
    window.setTimeout(function () {
        let exList = ['This', 'is', 'an', 'example'];

        exList.splice(1, 2)

        // Find the container where we will display the list
        let listContainer = document.getElementById('listContainer');

        // Join the list items into a single string separated by spaces
        listContainer.innerHTML = exList.join(' ');
    }, 100);  // Delay to ensure the HTML has rendered
</script>


```


<!-- A container to display the list -->
<div id="listContainer"></div>

<script>
    window.setTimeout(function () {
        let exList = ['This', 'is', 'an', 'example'];

        exList.splice(1, 2)

        // Find the container where we will display the list
        let listContainer = document.getElementById('listContainer');

        // Join the list items into a single string separated by spaces
        listContainer.innerHTML = exList.join(' ');
    }, 100);  // Delay to ensure the HTML has rendered
</script>




## Assigning and Adding Values

Values can also be assigned to a list. You can have an empty list and add values to it, or you can change values in a preexisting list.

Example of assigning a value


```python
%%js

let list3 = [1, 2, 3, 4, 5]

// assigns a different value to the element in position 4, changes 5 to 10
list3[4] = 10;
console.log(list3)

```


    <IPython.core.display.Javascript object>


Example of adding values


```python
%%js

// empty list
let list4 = []

// adds items
list4.push('I')
list4.push('II')
list4.push('III')

// print list
console.log(list4)
```

HTML example with both


```python
%%html
<!-- HTML output -->
<div id="output"></div>

<script>
    window.setTimeout(function () {
        let list5 = ['1'];
        
        // assigns/changes 1 to I
        list5[0] = 'I'
        
        // adds II and III
        list5.push('II')
        list5.push('III')

        // Find the container where we will display the list
        let output = document.getElementById('output');

        // Join the list items into a single string separated by spaces
        output.innerHTML = list5.join(', ');
    }, 100);  // Delay to ensure the HTML has rendered
</script>

```


<!-- A container to display the list -->
<div id="output"></div>

<script>
    window.setTimeout(function () {
        let list5 = ['1'];

        list5[0] = 'I'
        list5.push('II')
        list5.push('III')

        // Find the container where we will display the list
        let output = document.getElementById('output');

        // Join the list items into a single string separated by spaces
        output.innerHTML = list5.join(', ');
    }, 100);  // Delay to ensure the HTML has rendered
</script>



## Popcorn Hack 2

- Delete the last two items of the list below (delete1 and delete2)
- Change the non dessert item (fries) to a dessert
- Add two more desserts to list


```python
%%js

let desserts = ['cake', 'ice cream', 'cookies', 'fries', 'delete1', 'delete2']

console.log(desserts.join(", "))


```


    <IPython.core.display.Javascript object>

