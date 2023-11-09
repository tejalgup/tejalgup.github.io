---
layout: post
categories: gaming
---

# Random Agent Generator

Select an agent role o(〃＾▽＾〃)o: 
<select id="roleDropdown">
  <option value="All">All Agents</option>
  <option value="Duelist">Duelist</option>
  <option value="Initiator">Initiator</option>
  <option value="Controller">Controller</option>
  <option value="Sentinel">Sentinel</option>
  <option value="Custom">Custom</option>
</select>

<button id="generateButton">Pick an Agent!</button>

<div id="agentImageContainer">
  <div id="agentName"></div>
  <img id="agentImage" src="/assets/images/agents/Valorant.png" alt="Agent Image"></div>

<div id="agentMatrixContainer" class="agent-matrix-container"></div>


<script>

  function createAgentMatrix() {

  var duelistAgents = ["Jett", "Raze", "Phoenix", "Reyna", "Yoru", "Neon", "Iso"];
  var initiatorAgents = ["Sova", "Breach", "KAYO", "Skye", "Fade", "Gekko"];
  var controllerAgents = ["Brimstone", "Viper", "Omen", "Astra", "Harbor"];
  var sentinelAgents = ["Sage", "Cypher", "Killjoy", "Chamber", "Deadlock"];
  var agentArray = duelistAgents.concat(initiatorAgents, controllerAgents, sentinelAgents);


  var agentMatrixContainer = document.getElementById("agentMatrixContainer");
  agentMatrixContainer.innerHTML = ""; // Clear previous content

  allAgents.forEach(agent => {
    var button = document.createElement("button");
    button.className = "agent-button";

    // Create an image element for the agent
    var agentImage = document.createElement("img");
    agentImage.src = `https://static.valorantstats.xyz/agent-headshots/${agent.toLowerCase()}-headshot.png`;
    agentImage.alt = agent; // Use the agent's name as the alt text
    agentImage.className = "agent-image";

    // Create a div element for the agent's name
    var agentNameDiv = document.createElement("div");
    agentNameDiv.textContent = agent;
    agentNameDiv.className = "agent-name";

    // Add event listener to toggle agent inclusion in the array
    button.addEventListener("click", function() {
      var index = agentArray.indexOf(agent);
      if (index !== -1) {
        agentArray.splice(index, 1); // Remove agent from the array
        button.classList.remove("selected"); // Remove selected class
      } else {
        agentArray.push(agent); // Include agent in the array
        button.classList.add("selected"); // Add selected class
      }
    });

    // Append agent image and name to the button
    button.appendChild(agentImage);
    button.appendChild(agentNameDiv);

    agentMatrixContainer.appendChild(button);
  });
}




  // Array of Valorant agents' names

  var duelistAgents = ["Jett", "Raze", "Phoenix", "Reyna", "Yoru", "Neon", "Iso"];
  var initiatorAgents = ["Sova", "Breach", "KAYO", "Skye", "Fade", "Gekko"];
  var controllerAgents = ["Brimstone", "Viper", "Omen", "Astra", "Harbor"];
  var sentinelAgents = ["Sage", "Cypher", "Killjoy", "Chamber", "Deadlock"];
  var allAgents = duelistAgents.concat(initiatorAgents, controllerAgents, sentinelAgents);

  // Function to display a randomly selected agent from the chosen role
  function displayRandomAgent() {
    var selectedRole = document.getElementById("roleDropdown").value;
    var agentArray = [];

    // Determine the appropriate array based on the selected role
    if (selectedRole === "Custom") {
    createAgentMatrix(); // Show agent matrix for custom selection
    } else {

        if (selectedRole === "Duelist") {
        agentArray = duelistAgents;
        } else if (selectedRole === "Initiator") {
        agentArray = initiatorAgents;
        } else if (selectedRole === "Controller") {
        agentArray = controllerAgents;
        } else if (selectedRole === "Sentinel") {
        agentArray = sentinelAgents;
        } else if (selectedRole === "All") {
        agentArray = allAgents;
    }

    // Generate a random agent from the selected array
    var randomIndex = Math.floor(Math.random() * agentArray.length);
    var selectedAgent = agentArray[randomIndex];
    var imagePath = "/assets/images/agents/" + selectedAgent + ".png"
    
     // Set the agent name and image
    document.getElementById("agentName").textContent = "Selected Agent: " + selectedAgent;
    document.getElementById("agentImage").src = imagePath;

  }


 // Attach the function to the button click event
  document.getElementById("generateButton").addEventListener("click", displayRandomAgent);
</script>  
<style>
.agent-matrix-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.agent-button {
  width: 80px;
  height: 80px;
  cursor: pointer;
  border: none;
  background-size: cover;
}

.agent-button.selected {
  border: 2px solid #ff0000; /* Highlight selected buttons with a red border */
}
</style>