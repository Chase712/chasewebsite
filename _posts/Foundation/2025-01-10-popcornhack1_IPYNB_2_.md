---

---

---
Popcorn Hacks One
---

 - Delete the last two items of the list below (delete1 and delete2)
 - Change the non dessert item (fries) to a dessert
 - Add two more desserts to list


```python
let desserts = ['cake', 'ice cream', 'cookies', 'fries', 'delete1', 'delete2'];

// Remove the last two items
desserts.splice(-2);

// Change 'fries' to a dessert
desserts[desserts.indexOf('fries')] = 'brownies';

// Add two more desserts
desserts.push('pie', 'donuts');

console.log(desserts.join(", "));

```


      Cell In[7], line 1
        let desserts = ['cake', 'ice cream', 'cookies', 'fries', 'delete1', 'delete2'];
            ^
    SyntaxError: invalid syntax




```python
Popcorn hacks 2
```


```python
%%js
let my_list_2 = [3, 7, 9, 21]; // create a variable
const length = my_list_2.length; // create a const length
console.log(my_list_2); // print out your list
console.log(length); // print out the length of the list

```


    <IPython.core.display.Javascript object>



```python
instructions:
 - Create a length of a list and print it in console.log()
 - Create a variable called "list" or "my_list_2"
 - Create a list of numbers or words in the brackets [] Exp: let your_list = [3, 7, 9, 21];
 - Create a const length = your_list.length;
 - After all of that, finally print it out in console.log() Exp: console.log(your_list);
```
