Using AI to Build web3 Apps

Login to AI Tool

Prompt1:
Generate html, css and JavaScript for developing a simple calculator with additional features like backspace, percentage, and advanced mathematical operations (square root, power, and modulus). Also improved the layout and functionality.

How It Works:
HTML: The structure includes an input field for the display and buttons for digits, operators, and actions (clear and calculate).

CSS: Styles the calculator to make it visually appealing and responsive.

JavaScript: Handles the logic for appending values to the display, clearing the display, and performing calculations using the eval() function.

How to Run:
In the same folder, Save the HTML, CSS, and JavaScript code in their respective files (index.html, styles.css, script.js). 
Open the index.html file in a web browser to test.

Prompt2:
I  want to lauch this app on local blockchain using combination of Nodejs, truffle and Ganache. Give me the step guide of what to do.

Prerequisites
1. Node.js: Install from nodejs.org.
2. Truffle: Install globally using npm: - bash> npm install -g truffle
3.Ganache: Download and install from trufflesuite.com/ganache.
4. Metamask: Install the browser extension from metamask.io.

Step 1: Set Up the Project
1. Create a new directory for your project:
bash> mkdir calculator-dapp
cd calculator-dapp

2. Initialize a new Truffle project: bash> truffle init (This will create the following structure:)
calculator-dapp/
├── contracts/
├── migrations/
├── test/
└── truffle-config.js

3. Initialize a Node.js project: bash> npm init -y

4. Install required dependencies: bash> npm install web3 @truffle/contract

Step 2: Write the Smart Contract
1. Create a new smart contract in the contracts/ directory: bash> touch contracts/Calculator.sol

2. Add the following Solidity code to Calculator.sol:

   // SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Calculator {
    function add(uint256 a, uint256 b) public pure returns (uint256) {
        return a + b;
    }

    function subtract(uint256 a, uint256 b) public pure returns (uint256) {
        return a - b;
    }

    function multiply(uint256 a, uint256 b) public pure returns (uint256) {
        return a * b;
    }

    function divide(uint256 a, uint256 b) public pure returns (uint256) {
        require(b != 0, "Cannot divide by zero");
        return a / b;
    }
}

Step 3: Configure Truffle
Open truffle-config.js and update it to connect to Ganache:

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 7545, // Default Ganache port
      network_id: "*", // Match any network ID
    },
  },
  compilers: {
    solc: {
      version: "0.8.0", // Match your Solidity version
    },
  },
};

Step 4: Deploy the Smart Contract
1. Start Ganache and create a new workspace.

2. Compile the smart contract: bash> truffle compile

3. Deploy the contract to the local blockchain: bash> truffle migrate --network development (This will deploy the contract and provide the contract address. Save this address for later.)

Step 5: Set Up the Frontend
1. Create a public/ directory for your frontend files:
bash> mkdir public
cd public

2. Add your index.html, styles.css, and script.js files from the calculator app to the public/ directory.

3. Update script.js to interact with the smart contract:

   const contractAddress = "YOUR_CONTRACT_ADDRESS"; // Replace with your contract address
const abi = [ /* Paste the ABI from `build/contracts/Calculator.json` */ ];

let contract;
let account;

window.addEventListener("load", async () => {
    if (window.ethereum) {
        window.web3 = new Web3(window.ethereum);
        await window.ethereum.enable();
    } else {
        console.log("Please install MetaMask!");
    }

    contract = new web3.eth.Contract(abi, contractAddress);
    account = (await web3.eth.getAccounts())[0];
});

async function calculate() {
    const display = document.getElementById('display');
    const expression = display.value;

    try {
        let result;
        if (expression.includes('+')) {
            const [a, b] = expression.split('+');
            result = await contract.methods.add(parseInt(a), parseInt(b)).call({ from: account });
        } else if (expression.includes('-')) {
            const [a, b] = expression.split('-');
            result = await contract.methods.subtract(parseInt(a), parseInt(b)).call({ from: account });
        } else if (expression.includes('*')) {
            const [a, b] = expression.split('*');
            result = await contract.methods.multiply(parseInt(a), parseInt(b)).call({ from: account });
        } else if (expression.includes('/')) {
            const [a, b] = expression.split('/');
            result = await contract.methods.divide(parseInt(a), parseInt(b)).call({ from: account });
        } else {
            result = "Invalid operation";
        }
        display.value = result;
    } catch (error) {
        display.value = 'Error';
    }
}

Step 6: Serve the Frontend
1. Install a simple HTTP server: bash> npm install -g http-server

2. Serve the public/ directory: bash> http-server public

3. Open your browser and navigate to http://localhost:8080.

Step 7: Connect to MetaMask
1. Open MetaMask and connect to the Ganache network:

      Network Name: Ganache

      RPC URL: http://127.0.0.1:7545

      Chain ID: 1337

2. Import an account from Ganache using its private key.

Step 8: Test the App
1. Open the calculator app in your browser.

2. Perform calculations (e.g., 2 + 3).

3. The result will be computed by the smart contract on the blockchain.

Summary
Smart Contract: Handles arithmetic operations.

Frontend: Interacts with the contract using Web3.js.

Ganache: Provides a local blockchain for testing.

MetaMask: Connects the frontend to the blockchain.




