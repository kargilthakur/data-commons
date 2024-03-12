[Data Commons](../)

# Good Paying Jobs

Goal 1. No Poverty - Good Paying Jobs and Assistance

<style>
    body {
      font-family: 'Arial', sans-serif;
      margin: 20px;
      padding: 20px;
    }

    button {
      background-color: #4CAF50;
      color: white;
      padding: 10px 15px;
      margin: 10px 0;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    label {
      display: block;
      margin: 10px 0;
    }

    input {
      padding: 8px;
      width: 100%;
      box-sizing: border-box;
      margin-bottom: 10px;
    }

    #resultContainer {
      margin-top: 20px;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
    }

    .suggestion-container {
      margin-top: 5px;
    }

    .suggestion-bubble {
      display: inline-block;
      padding: 5px 10px;
      margin-right: 5px;
      cursor: pointer;
      border-radius: 4px;
      border: 1px solid white; /* Changed border color to white */
    }

    .suggestion-bubble:hover {
      background-color: yellow;
    }
  </style>

## Usage Example

<button id="loadDataButton">Load Data Commons</button>

<div>
  <label for="dcidInput">Enter DCID:</label>
  <div class="suggestion-container" id="dcidSuggestions">
    <span class="suggestion-bubble">geoId/06</span>
    <span class="suggestion-bubble">geoId/07</span>
    <span class="suggestion-bubble">geoId/08</span>
    <!-- Add more suggestion bubbles here -->
  </div>
  <input type="text" id="dcidInput" placeholder="e.g., geoId/06">
</div>

<div>
  <label for="propertyInput">Enter Property:</label>
  <div class="suggestion-container" id="propertySuggestions">
    <span class="suggestion-bubble"><-</span>
    <span class="suggestion-bubble">-></span>
    <!-- Add more suggestion bubbles here -->
  </div>
  <input type="text" id="propertyInput" placeholder="e.g., <-">
</div>

<div id="resultContainer"></div>

<button id="downloadButton">Download JSON</button>

```js
  function addSuggestionToInput(suggestion, inputId) {
    document.getElementById(inputId).value = suggestion;
  }

  // Event listeners for suggestion bubbles
  document.querySelectorAll('.suggestion-bubble').forEach(item => {
    item.addEventListener('click', event => {
      // Get the suggestion bubble text
      const suggestion = event.target.innerText;
      // Get the corresponding input field id
      const inputId = event.target.parentNode.nextElementSibling.id;
      // Add suggestion to the input field
      addSuggestionToInput(suggestion, inputId);
    });
  });
```

```js
  import {loadDataCommons,displayJsonData} from "./data_loader.js";
```

```js
  document.getElementById('loadDataButton').addEventListener('click', () => 
    {
        const apiKey = 'AIzaSyCTI4Xz-UW_G2Q2RfknhcfdAnTHq5X5XuI';
        const dcidInput = document.getElementById('dcidInput').value;
        const propertyInput = document.getElementById('propertyInput').value;

        console.log('DCID:', dcidInput);
        console.log('Property:', propertyInput);

        loadDataCommons(apiKey, dcidInput, propertyInput).then(data => {
            console.log(data);
            displayJsonData(data);
            })
                .catch(error => {
                    console.error('Error loading data:', error);
            });
        
    }
  );
```

```js
  // Download JSON button click event
  document.getElementById("downloadButton").addEventListener("click", function() {
    const resultData = document.getElementById("resultContainer").textContent;
    const data = "data:text/json;charset=utf-8," + encodeURIComponent(resultData);
    const downloadButton = document.createElement("a");
    downloadButton.setAttribute("href", data);
    downloadButton.setAttribute("download", "data.json");
    downloadButton.click();
  });
```
