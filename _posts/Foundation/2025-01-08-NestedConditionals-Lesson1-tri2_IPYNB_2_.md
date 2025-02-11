---
layout: post
title: Nested Conditionals, Part One
description: Introducing nested conditionals
type: issues
comments: True
---

<h1>Conditionals</h1>

Conditionals in coding are if/else statements. They are used to determine what an output should be used for a given input. For example, if you have enough tickets, you can buy a prize - but if you don't, you can't buy it.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let tickets = 5 //the message you get depends on this value
        
        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (tickets >= 10){
            displayMessage("You can get this prize!");
        } else {
            displayMessage("Sorry, you don't have enough tickets for this prize.");
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
        let tickets = 5 //the message you get depends on this value

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if (tickets >= 10){
            displayMessage("You can get this prize!");
        } else {
            displayMessage("Sorry, you don't have enough tickets for this prize.");
        }

    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>



<h1>Nested Conditionals</h1>

Nested conditionals are when you have if/else statements inside an if/else statement, making them "nested" inside one another. If you fufill the requirement for one loop, you go to the next; if you don't fufill the requirement for the loop, then you're prevented from going forward.

Using nested conditionals makes it so you can have more outcomes that were affected by whether or a certain value was reached or what else you're checking in a loop. For example, the code below has three different possible outcomes depending on the factors given.


```python
%%html
<!-- HTML output div -->
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        //Can change both of these values to get a different outcome
        let tickets = 10 
        let minutesLeft = 30
        
        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if(tickets >= 10){
            if(minutesLeft >= 45){
                displayMessage("You have enough time and tickets to go on one more ride.");
            } else {
                displayMessage("You don't have enough time to do anything! Maybe save your tickets for next time.");
            }
        } else {
            displayMessage("Sorry! You don't have enough tickets to do anything.");
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
        //Can change both of these values to get a different outcome
        let tickets = 10 
        let minutesLeft = 30

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        if(tickets >= 10){
            if(minutesLeft >= 45){
                displayMessage("You have enough time and tickets to go on one more ride.");
            } else {
                displayMessage("You don't have enough time to do anything! Maybe save your tickets for next time.");
            }
        } else {
            displayMessage("Sorry! You don't have enough tickets to do anything.");
        }

    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>


