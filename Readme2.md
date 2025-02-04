How do I open this web3 app?

To open and interact with your **Web3 calculator app**, follow these steps. This guide assumes you've already set up the app using **Node.js**, **Truffle**, **Ganache**, and **MetaMask** as described in the previous steps.

---

### Step 1: Start Ganache
1. Open **Ganache**.
2. Create a new workspace or use the default one.
3. Ensure Ganache is running on `http://127.0.0.1:7545`.

---

### Step 2: Serve the Frontend
1. Open a terminal in your project directory.
2. Navigate to the `public/` folder where your frontend files (`index.html`, `styles.css`, `script.js`) are located.
3. Start a local HTTP server using `http-server`:
   ```bash
   http-server
   ```
   This will start the server and provide a URL, typically:
   ```
   http://127.0.0.1:8080
   ```

---

### Step 3: Open the App in a Browser
1. Open your browser (preferably Chrome or Firefox with MetaMask installed).
2. Navigate to the URL provided by `http-server` (e.g., `http://127.0.0.1:8080`).

---

### Step 4: Connect MetaMask to Ganache
1. Open the **MetaMask** browser extension.
2. Click on the network dropdown (usually says "Ethereum Mainnet").
3. Select **Custom RPC** and enter the following details:
   - **Network Name**: Ganache
   - **New RPC URL**: `http://127.0.0.1:7545`
   - **Chain ID**: `1337`
   - **Currency Symbol**: ETH
4. Save the network.

---

### Step 5: Import an Account from Ganache
1. In **Ganache**, copy the private key of one of the accounts.
2. In **MetaMask**, click on the account icon (top-right corner).
3. Select **Import Account**.
4. Choose **Private Key** and paste the private key from Ganache.
5. Click **Import**.

---

### Step 6: Interact with the Calculator App
1. Once the app is open in your browser, you should see the calculator interface.
2. Perform calculations (e.g., `2 + 3`).
3. When you click the `=` button, the app will:
   - Send a transaction to the smart contract (if necessary).
   - Display the result on the screen.

---

### Troubleshooting
1. **MetaMask Not Connected**:
   - Ensure MetaMask is connected to the Ganache network.
   - Check if the app is running on `http://localhost:8080` (not `https`).

2. **Transactions Not Working**:
   - Ensure you have enough ETH in your MetaMask account (Ganache provides test ETH).
   - Check the browser console for errors.

3. **Smart Contract Not Deployed**:
   - Verify that the contract is deployed using `truffle migrate --network development`.
   - Ensure the contract address in `script.js` is correct.

4. **Browser Compatibility**:
   - Use a browser with MetaMask support (Chrome, Firefox, Brave).

---

### Example Workflow
1. Open the app at `http://127.0.0.1:8080`.
2. Enter `5 * 3` in the calculator.
3. Click `=`.
4. MetaMask will prompt you to confirm the transaction.
5. Once confirmed, the result (`15`) will appear on the screen.

---

### Summary
- **Ganache**: Provides the local blockchain.
- **MetaMask**: Connects your browser to the blockchain.
- **HTTP Server**: Serves the frontend files.
- **Smart Contract**: Handles the calculations.

Let me know if you encounter any issues! 😊
