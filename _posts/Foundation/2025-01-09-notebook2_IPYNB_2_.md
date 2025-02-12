---

---

Length of a List
In JavaScript, the length of a list (also known as an array) refers to the number of elements it contains. It can be accessed using the (.length) property, which shows the total number of elements in the array.

Display List <br>
Number Example:


```python
%%js

let list = [2, 4, 6, 8, 10];//These are things what will be shown on the list
const length = list.length; //length will be 5 since 5 elements in list
console.log(list);//This will show the list 
```


    <IPython.core.display.Javascript object>


Array indexOf() <br>
This does the job of searching for an element and finds its position within the array <br>
ex: 


```python
%%js

const exarray = ["a", "b", "c", "b", "d"];

console.log(exarray.indexOf("a"));    // Output: 0 (0, first a is the first letter (base 10 starts at 0 or something idk lol))
console.log(exarray.indexOf("b"));    // Output: 1 (1, first b is the second letter)
console.log(exarray.indexOf("c"));    // Output: 2 (so on and so forth, you can do the rest)
console.log(exarray.indexOf("d"));    // Output: 4
console.log(exarray.indexOf("z"));    // Output: -1 (not found)

```


    <IPython.core.display.Javascript object>


Array lastIndexOf() <br>
similar to Array indexOf() but returns last time the object has appeared <br>
ex:


```python
%%js

const exarray = ["a", "b", "c", "b", "d"];

console.log(exarray.indexOf("a"));    // Output: 0 (0, first a is the first letter (base 10 starts at 0 or something idk lol))
console.log(exarray.indexOf("b"));    // Output: 1 (1, first b is the second letter)
console.log(exarray.indexOf("c"));    // Output: 2 (so on and so forth, you can do the rest)
//heres the last index of
console.log(exarray.lastIndexOf("b"));    // Output: 3 (3, last b is the fourth letter)
console.log(exarray.indexOf("z"));    // Output: -1 (not found)

```


    <IPython.core.display.Javascript object>


Array.includes() <br>
Finds an element in the array <br>
ex:


```python
%%js 
let list = ['a', 'b', 'c'];
let hasa = list.includes('a');  // Check if 'a' is in the array
console.log(hasa);  // Output: true
```


    <IPython.core.display.Javascript object>


refrences: <br>
https://www.w3schools.com/js/js_array_search.asp
