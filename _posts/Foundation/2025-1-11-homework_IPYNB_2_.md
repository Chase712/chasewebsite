---

---

# Lesson 1 Homework


```python
let desserts = ["lemon","delete1","ice cream","chocolate cake","key lime pie","delete2"];
desserts.pop(); // which command gets rid of the last element in the array?
desserts.splice(1, 1); // which command will delete the delete1 element and how do you use it??

// now that that's done... a lemon isn't a dessert unless you're weird... maybe change it to a lemon-themed dessert?
desserts[0] = "lemon tart"; // put your lemon-themed dessert here :D

// okay okay, you've proven your skills... now all that's left is to print the list!
console.log(desserts);

```


      Cell In[2], line 5
        // now that that's done... a lemon isn't a dessert unless you're weird... maybe change it to a lemon-themed dessert?
                                                                     ^
    SyntaxError: unterminated string literal (detected at line 5)



# Lesson 2 Homework - Part 1


```python
// Step 1: Create a list with a repeating element
let list = [1, 2, 3, 1, 4];

// Step 2: Use a for loop to iterate through each element and print the index of them
for (let i = 0; i < list.length; i++) {
  console.log(`Index ${i}: ${list[i]}`);
}

// Step 3: Find and print the index of the last occurrence of the repeated value
let lastIndex = list.lastIndexOf(1); // Replace '1' with your repeated value
console.log(`The last occurrence of the repeated value is at index: ${lastIndex}`);

```


      Cell In[8], line 1
        // Step 1: Create a list with a repeating element
        ^
    SyntaxError: invalid syntax



# Lesson 2 Homework - Part 2


```python
// Step 1: Create a list
let list = ["apple", "banana", "cherry", "date"];

// Step 2: Print the length of your list
console.log(list.length); // Outputs the number of elements in the list

// Step 3: Check if a value is included in the list
let isIncluded = list.includes("banana"); // Change "banana" to test other values
console.log(isIncluded); // Outputs true or false

```


      Cell In[4], line 1
        // Step 1: Create a list
        ^
    SyntaxError: invalid syntax



You're done with your homework!!
