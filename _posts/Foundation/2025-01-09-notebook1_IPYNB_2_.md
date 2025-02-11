---

---

Hi there!
Today, we'll be teaching you all about arrays!!

Arrays are variables that store a list of elements. In our example, we will have the list of the numbers 1-5.

We create it like so:




```python
let list = [1, 2, 3, 4, 5];
//When we refer to an element in our array, we start with list[0].
//In this case:

list[0] = 1
list[1] = 2
list[2] = 3, etc.


```


We can output any element from our list using the console.log function.
For example:





```python
let list2 = [1, 2, 3, 4, 5];

console.log(list2[0]); //prints 1 as it is the first element in the array
console.log(list2[1]); //prints 2
console.log(list2[2]); //prints 3
console.log(list2[3]); //prints 4
console.log(list2[4]); //prints 5



```

To delete elements, we can use the pop() or splice() functions:

pop() removes the last element of an array.
splice(index, count) removes an element at a specified index. The count parameter tells how many elements to remove.




```python
let list3 = [1, 2, 3, 4, 5];

list3.pop(); //deletes the last value (5) in the list
console.log(list3); //[1, 2, 3, 4]

list3.splice(3, 1); //deletes the 4th element (index 3), which is 4
console.log(list3); //[1, 2, 3]


```

We can also update or assign values to elements in an array.

For example:




```python
let list4 = [1, 2, 3, 4, 5];

list4[2] = 6; //changes the value at index 2 from 3 to 6
console.log(list4); // [1, 2, 6, 4, 5]
//To add values to an array, we use the push() function.
//Here’s how we can add elements:

%%javascript
let list5 = []; //creates an empty list

list5.push(1);
list5.push(2);
list5.push(3);

console.log(list5); // [1, 2, 3]
```

refrences: <br>
if you find our teaching to be not great then you can always use these resources <br>
they have kinda?? been vetted by rachit :D <br>
https://www.w3schools.com/js/js_arrays.asp  <br>
https://www.w3schools.com/js/js_array_methods.asp  <br>
