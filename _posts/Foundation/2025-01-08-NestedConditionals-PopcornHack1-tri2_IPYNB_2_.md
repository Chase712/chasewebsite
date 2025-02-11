---
layout: post
title: Nested Conditionals, Popcorn Hack One
description: First popcorn hack for nested conditonals
type: issues
comments: True
---

### Popcorn Hack 1

This code has the option to let the player go on a ride of their choosing, and either lets them go on the ride or does not let them go on the ride based on their amount of tickets that they have. Try adding some code that makes it so that the code also takes into account the height of the person trying to ride the ride and have it be another constraint that determines whether or not the person goes on a ride.


```python
<div id="message"></div>
<script>
    function runWhenDOMLoaded() {
        let ticketAmount = 60; // Ticket amount
        let height = 120; // Height of the person (in cm)
        let ride = "Ferris Wheel"; // Ride choice

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(a, h) { // Add height parameter
            if (ticketAmount >= a) {
                if (h >= 120) { // Check if height is enough
                    displayMessage("You have enough tickets and meet the height requirement! Enjoy the ride! :D");
                } else {
                    displayMessage("You're not tall enough for the ride... :(");
                }
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60, height); // Pass height as an argument
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40, height); // Pass height as an argument
        }
    }

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
        let ticketAmount = 60; // Makes the ticket amount be 60, make another variable for height
        let ride = "Ferris Wheel"; // sets the ride that the person wants to ride on

        const messageElement = document.getElementById("message");

        function displayMessage(message) {
            console.log(message); // Log to console
            messageElement.textContent = message; // Display on the webpage
        }

        function enoughTickets(a) {//Add another parameter for height, maybe change the name of the parameter
            if (ticketAmount >= a) {
                displayMessage("You have enough tickets! Yay! :D");//make another if else statement inside of this to check for height
            } else {
                displayMessage("You don't have enough tickets... :(");
            }
        }

        if (ride === "Roller Coaster") {
            enoughTickets(60); //Nests the function and the conditionals
        } else if (ride === "Ferris Wheel") {
            enoughTickets(40);
        }    
    }

    // Ensure the function runs only after the page loads
    if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", runWhenDOMLoaded);
    } else {
        runWhenDOMLoaded();
    }
</script>


