---
layout: post
categories: gaming
---

# Random Agent Generator

Select an agent role o(〃＾▽＾〃)o: 

<button id="generateButton">Pick an Agent!</button>



<div id="agentMatrixContainer" class="agent-matrix-container"></div>

<div id="agentImageContainer">
  <div id="agentName"></div>
  <img id="agentImage" src="/assets/images/agents/Valorant.png" alt="Agent Image"></div>

<script>

  var agentRoles = {
    Duelist: ["Jett", "Raze", "Phoenix", "Reyna", "Yoru", "Neon", "Iso"],
    Initiator: ["Sova", "Breach", "KAYO", "Skye", "Fade", "Gekko"],
    Controller: ["Brimstone", "Viper", "Omen", "Astra", "Harbor"],
    Sentinel: ["Sage", "Cypher", "Killjoy", "Chamber", "Deadlock"]
  };

  var selectedAgents = [];


function createAgentMatrix() {
    var agentMatrixContainer = document.getElementById("agentMatrixContainer");

      // Iterate through each role in agentRoles
    Object.keys(agentRoles).forEach(role => {
    // Create a new row (div) for the current role
    var roleRow = document.createElement("div");
    roleRow.className = "role-row";


        // Create a button to toggle agents of this role
        var toggleButton = document.createElement("button");
        toggleButton.className = "toggle-button";
        toggleButton.addEventListener("click", function() {
            var roleAgents = agentRoles[role];
            var shouldSelect = !roleAgents.every(agent => selectedAgents.includes(agent));
            if (shouldSelect) {
                selectedAgents.push(...roleAgents);
            } else {
                roleAgents.forEach(agent => {
                    var index = selectedAgents.indexOf(agent);
                    if (index !== -1) {
                        selectedAgents.splice(index, 1);
                    }
                });
            }
            createAgentMatrix(); // Re-create the matrix after toggling
        });

        // Set toggle button image based on role
        var roleIcon = document.createElement("img");
        roleIcon.className = "role-icon";
        var roleIconURL = `https://static.valorantstats.xyz/role-icons/${role.toLowerCase()}-icon.png`;
        roleIcon.src = roleIconURL;
        
        toggleButton.appendChild(roleIcon);
        roleRow.appendChild(toggleButton);
        
    agentRoles[role].forEach(agent => {
      var button = document.createElement("button");
      button.className = "agent-button";

      var agentImage = document.createElement("img");
      agentImage.src = `https://static.valorantstats.xyz/agent-headshots/${agent.toLowerCase()}-headshot.png`;
      agentImage.alt = agent;
      agentImage.className = "agent-image";

      var agentNameDiv = document.createElement("div");
      agentNameDiv.textContent = agent;
      agentNameDiv.className = "agent-name";

    // Add agents to the selectedAgents array and toggle corresponding buttons
      selectedAgents.push(agent);
      button.classList.add("selected");


      button.addEventListener("click", function() {
        var index = selectedAgents.indexOf(agent);
        if (index !== -1) {
          selectedAgents.splice(index, 1);
          button.classList.remove("selected");
        } else {
          selectedAgents.push(agent);
          button.classList.add("selected");
        }
      });

      if (selectedAgents.includes(agent)) {
        button.classList.add("selected");
      }

      button.appendChild(agentImage);
      button.appendChild(agentNameDiv);
      roleRow.appendChild(button);
    });
    agentMatrixContainer.appendChild(roleRow);
    });
  }

createAgentMatrix();

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