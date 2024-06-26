---
layout: post
categories: gaming
---

# Random Agent Generator

Select an agents! Click role icon to toggle row on/off o(〃＾▽＾〃)o: 

<button id="generateButton">Pick an Agent!</button>

<div id="agentMatrixContainer" class="agent-matrix-container"></div>

<div id="agentImageContainer">
  <div id="agentName"></div>
  <img id="agentImage" src="/assets/images/agents/Valorant.png" alt="Agent Image"></div>

<script>

  var agentRoles = {
    Duelist: [ "Iso", "Jett", "Neon", "Phoenix", "Raze", "Reyna", "Yoru"],
    Initiator: ["Breach", "Fade", "Gekko", "KAYO", "Skye", "Sova"],
    Controller: ["Astra", "Brimstone", "Clove", "Harbor", "Omen", "Viper"],
    Sentinel: ["Chamber", "Cypher", "Deadlock", "Killjoy", "Sage"]
  };

  var selectedAgents = [];
// Initialize selectedAgents with all agents
  Object.keys(agentRoles).forEach(role => {
    selectedAgents.push(...agentRoles[role]);
  });


function toggleRoleAgents(role) {
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
}

function createAgentMatrix() {
    var agentMatrixContainer = document.getElementById("agentMatrixContainer");
    agentMatrixContainer.innerHTML = ''; // Clear the container before re-populating

      // Iterate through each role in agentRoles
    Object.keys(agentRoles).forEach(role => {
    // Create a new row (div) for the current role
    var roleRow = document.createElement("div");
    roleRow.className = "role-row";


        // Create a button to toggle agents of this role
        var toggleButton = document.createElement("button");
        toggleButton.className = "toggle-button";
        toggleButton.addEventListener("click", function() {
            toggleRoleAgents(role);
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
    var agentNameElement = document.getElementById("agentName");
    var agentImageElement = document.getElementById("agentImage");

    if (selectedAgents.length === 0) {
      // No agents selected, display a message and set the initial Valorant image
      agentNameElement.textContent = "";
      agentImageElement.src = "/assets/images/agents/Valorant.png";
    } else {
    // Generate a random agent from the selected array
      var randomIndex = Math.floor(Math.random() * selectedAgents.length);
      var selectedAgent = selectedAgents[randomIndex];
      var imagePath = "/assets/images/agents/" + selectedAgent + ".png";

      // Set the agent name and image
      agentNameElement.textContent = "Selected Agent: " + selectedAgent;
      agentImageElement.src = imagePath;
    }
  }

  // Attach the function to the button click event
  document.getElementById("generateButton").addEventListener("click", displayRandomAgent);

  // Attach the toggle function to the role toggle button click events
  document.getElementById("toggleDuelist").addEventListener("click", function() {
    toggleRoleAgents("Duelist");
  });
  document.getElementById("toggleInitiator").addEventListener("click", function() {
    toggleRoleAgents("Initiator");
  });
  document.getElementById("toggleController").addEventListener("click", function() {
    toggleRoleAgents("Controller");
  });
  document.getElementById("toggleSentinel").addEventListener("click", function() {
    toggleRoleAgents("Sentinel");
  });
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

.role-icon {
  width: 75px; /* Set the width to match the agent images */
  height: 75px; /* Set the height to match the agent images */
}

.agent-button.selected {
  border: 2px solid #ff0000; /* Highlight selected buttons with a red border */
}
</style>
