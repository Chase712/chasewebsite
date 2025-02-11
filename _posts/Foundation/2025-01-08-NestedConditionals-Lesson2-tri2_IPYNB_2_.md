---
layout: post
title: Nested Conditionals, Part Two
description: Nested Conditionals with Booleans
type: issues
comments: True
---

# Nested Conditionals with Booleans

A boolean is a data type that has only two possible values: true and false.

Here is an example of a nested conditional with booleans. At an amusement park, you need to be a certain height and age to go on some rides. This code checks if a person meets those requirements and can go on the ride.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let isTallEnough = true;  // Boolean: Is the visitor tall enough?
        let isOldEnough = false;  // Boolean: Is the visitor old enough?

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (isTallEnough) { // Outer condition: visitor meets the height requirement
            if (isOldEnough) { // Nested condition: visitor meets the age requirement
                displayMessage("You can go on all rides!");
            } else {
                displayMessage("You can go on most rides, but not the adult ones.");
            }
        } else {
            displayMessage("Sorry, you don't meet the height requirement for any rides.");
        }    
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>

```


<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let isTallEnough = true;  // Boolean: Is the visitor tall enough?
        let isOldEnough = false;  // Boolean: Is the visitor old enough?

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (isTallEnough) { // Outer condition: visitor meets the height requirement
            if (isOldEnough) { // Nested condition: visitor meets the age requirement
                displayMessage("You can go on all rides!");
            } else {
                displayMessage("You can go on most rides, but not the adult ones.");
            }
        } else {
            displayMessage("Sorry, you don't meet the height requirement for any rides.");
        }    
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>



Two variables are defined at the beginning of the code: isTallEnough and isOldEnough. Each is set to a boolean value. The first conditional checks the value of isTallEnough to see if it is true or false, and if it is true, it goes on to the next conditional to check the value of isOldEnough. If isTallEnough is false, it doesn't check the age and prints that you aren't tall enough.

Here is another example of nested conditionals. This time, it includes both boolean and integers. This code checks if the weather is suitable to go on the rides, if the person has a priority pass, and how long the line is to let you know which rides you can go on and how long you have to wait.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let isWeatherGood = true;       // Boolean: Is the weather suitable for outdoor rides?
        let hasPriorityPass = false;    // Boolean: Does the visitor have a priority pass?
        let line = 60;           // Integer: Number of available seats on the ride.
        
        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (isWeatherGood) {
            // Check if the weather is good for outdoor rides
            displayMessage("Outdoor rides are open!");

            if (line > 30) {
                // Check how long the line is
                if (hasPriorityPass) {
                    // Check if the visitor has a priority pass
                    displayMessage("You can skip the line with your priority pass!");
                } else {
                    // Visitor doesn't have a priority pass but seats are available
                    displayMessage("You can enjoy the ride, but you'll need to wait in line.");
                }
            } else {
                // Line doesn't have a very long line
                displayMessage("The ride doesn't have a very long line, have fun :)");
            }
        } else {
            // If the weather is not good, outdoor rides are closed
            displayMessage("Outdoor rides are closed due to weather conditions.");
        }
    
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>

```


<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let isWeatherGood = true;       // Boolean: Is the weather suitable for outdoor rides?
        let hasPriorityPass = false;    // Boolean: Does the visitor have a priority pass?
        let line = 60;           // Integer: Number of available seats on the ride.

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (isWeatherGood) {
            // Check if the weather is good for outdoor rides
            displayMessage("Outdoor rides are open!");

            if (line > 30) {
                // Check how long the line is
                if (hasPriorityPass) {
                    // Check if the visitor has a priority pass
                    displayMessage("You can skip the line with your priority pass!");
                } else {
                    // Visitor doesn't have a priority pass but seats are available
                    displayMessage("You can enjoy the ride, but you'll need to wait in line.");
                }
            } else {
                // Line doesn't have a very long line
                displayMessage("The ride doesn't have a very long line, have fun :)");
            }
        } else {
            // If the weather is not good, outdoor rides are closed
            displayMessage("Outdoor rides are closed due to weather conditions.");
        }

    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>


