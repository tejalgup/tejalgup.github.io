---
layout: post
categories: gaming
---

# Random Agent Generator

Select an agent role o(〃＾▽＾〃)o: 

<button id="generateButton">Pick an Agent!</button>

<div id="agentImageContainer">
  <div id="agentName"></div>
  <img id="agentImage" src="/assets/images/agents/Valorant.png" alt="Agent Image"></div>

<div id="agentMatrixContainer" class="agent-matrix-container"></div>


<script>

  var agentRoles = {
    Duelist: ["Jett", "Raze", "Phoenix", "Reyna", "Yoru", "Neon", "Iso"],
    Initiator: ["Sova", "Breach", "KAYO", "Skye", "Fade", "Gekko"],
    Controller: ["Brimstone", "Viper", "Omen", "Astra", "Harbor"],
    Sentinel: ["Sage", "Cypher", "Killjoy", "Chamber", "Deadlock"]
  };

  var selectedAgents = [];


function createAgentMatrix(role) {

  var agentMatrixContainer = document.getElementById("agentMatrixContainer");
  agentMatrixContainer.innerHTML = ""; // Clear previous content

  agentRoles[role].forEach(agent => {
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

    // Add event listener to toggle agent inclusion in the selectedAgents array
    button.addEventListener("click", function() {
      var index = selectedAgents.indexOf(agent);
      if (index !== -1) {
        selectedAgents.splice(index, 1); // Remove agent from selectedAgents array
        button.classList.remove("selected"); // Remove selected class
      } else {
        selectedAgents.push(agent); // Add agent to selectedAgents array
        button.classList.add("selected"); // Add selected class
      }
    });

    // Check if agent is already selected and add selected class
    if (selectedAgents.includes(agent)) {
      button.classList.add("selected");
    }

    // Append agent image and name to the button
    button.appendChild(agentImage);
    button.appendChild(agentNameDiv);

    agentMatrixContainer.appendChild(button);
  });
}
createAgentMatrix("Duelist");
createAgentMatrix("Initiator");
createAgentMatrix("Controller");
createAgentMatrix("Sentinel");

  // Function to display a randomly selected agent from the chosen role
  function displayRandomAgent() {

    

    // Generate a random agent from the selected array
    var randomIndex = Math.floor(Math.random() * selectedAgents.length);
    var selectedAgent = selectedAgents[randomIndex];
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