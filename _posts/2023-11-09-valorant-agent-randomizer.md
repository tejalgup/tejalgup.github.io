---
layout: post
categories: gaming
---

# Random Number Generator

Click the button to generate a random number between 1 and 23:

<button id="generateButton">Generate Random Number</button>
<div id="randomNumber"></div>

<script>
  // Function to generate and display a random number between 1 and 23
  function generateRandomNumber() {
    // Generate a random number between 1 and 23
    var randomNumber = Math.floor(Math.random() * 23) + 1;
    document.getElementById("randomNumber").innerHTML = "Random Number: " + randomNumber;
  }

  // Attach the function to the button click event
  document.getElementById("generateButton").addEventListener("click", generateRandomNumber);
</script>
