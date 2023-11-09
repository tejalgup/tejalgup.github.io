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
</select>

<button id="generateButton">Pick an Agent!</button>

<div id="agentImageContainer">
  <div id="agentName"></div>
  <img id="agentImage" src="/assets/images/agents/Valorant.png" alt="Agent Image"></div>


<script>

  

  var duelistAgents = ["Jett", "Raze", "Phoenix", "Reyna", "Yoru", "Neon", "Iso"];
  var initiatorAgents = ["Sova", "Breach", "KAYO", "Skye", "Fade", "Gekko"];
  var controllerAgents = ["Brimstone", "Viper", "Omen", "Astra", "Harbor"];
  var sentinelAgents = ["Sage", "Cypher", "Killjoy", "Chamber", "Deadlock"];
  var allAgents = duelistAgents.concat(initiatorAgents, controllerAgents, sentinelAgents);

  // Function to display a randomly selected agent from the chosen role
  function displayRandomAgent() {
    var selectedRole = document.getElementById("roleDropdown").value;
    var agentArray = [];

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