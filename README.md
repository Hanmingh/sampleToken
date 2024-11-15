# ERC-20 Token Deployment with Hardhat

This project demonstrates the deployment of a basic ERC-20 token using Hardhat, a development environment for Ethereum. It includes a sample contract, tests for that contract, instructions on how to deploy the contract to a live Ethereum test network (e.g., Sepolia), and how to verify the contract on Etherscan.

## Prerequisites

Before you begin, make sure you have the following:

1. **Ethereum Wallet**  
   Install [MetaMask](https://metamask.io/) or [Coinbase Wallet](https://www.coinbase.com/wallet) to manage your ETH and test ETH for deployment on the Sepolia network.  
   - These wallets allow you to manage assets on multiple networks, including the Ethereum mainnet and test networks like Sepolia.
   - You will also need test ETH to deploy contracts on Sepolia. You can obtain test ETH from the Sepolia faucet at [Alchemy's Ethereum Sepolia Faucet](https://www.alchemy.com/faucets/ethereum-sepolia).  
   **Note**: Ensure you are using a test network (like Sepolia) when dealing with test ETH to avoid using real funds.

2. **Git**  
   Ensure you have Git installed on your system for cloning repositories. You can download it from [here](https://git-scm.com/).

3. **Infura API Key**  
   Sign up for [Infura](https://infura.io/) and create a new project. Obtain an API key that will allow you to interact with the Ethereum network via Sepolia.

4. **Environment Variables**  
   Add your MetaMask or Coinbase Wallet's private key (SEPOLIA_PRIVATE_KEY) and the Infura API key to your environment variables.  
   **Warning:** Never use real ETH in test environments or expose your private key publicly. Use only test networks like Sepolia.

### Set Configuration Variables

To make your development environment easier to manage, Hardhat allows setting configuration variables, including your private keys and API keys, directly through the command line.

1. **Set the Infura API Key and Sepolia Private Key:**

    ```bash
    npx hardhat vars set INFURA_API_KEY
    npx hardhat vars set SEPOLIA_PRIVATE_KEY
    ```
2.	**Get a Configuration Variable:**

    If you need to check the value of any configuration variable, use the following command:
    ```bash
    npx hardhat vars get TEST_API_KEY
    ```

3.	**List All Configuration Variables:**

    ```bash
    npx hardhat vars list
    ```
4.	**Remove a Configuration Variable:**

    ```bash
    npx hardhat vars delete TEST_API_KEY
    ```

## Setting Up the Development Environment

1. **Install Node.js & npm**

   Use Node Version Manager (NVM) to install Node.js (v22):

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   nvm install 22
   nvm use 22
   nvm alias default 22
   npm install npm --global # Upgrade npm to the latest version
   ```

2. **Initialize the Project and Install Hardhat**

   Set up your project directory, then initialize npm and install Hardhat:

   ```bash
   mkdir erc20-project
   cd erc20-project
   npm init -y
   npm install --save-dev hardhat
   ```

3. **Create and Compile Smart Contracts**

   Use Hardhat to create a new project, and then compile the smart contracts:

   ```bash
   npx hardhat init
   npx hardhat compile
   ```

4. **Run Tests**

   Write and execute tests to ensure the contract behaves as expected:

   ```bash
   npx hardhat test
   ```

   To report gas usage during tests:

   ```bash
   REPORT_GAS=true npx hardhat test
   ```

## Deployment

1. **Run a Local Ethereum Node**

   If needed, you can simulate Ethereum locally by spinning up a Hardhat node:

   ```bash
   npx hardhat node
   ```

2. **Deploy to Sepolia Test Network**

   When ready to deploy to Sepolia, ensure that your configuration includes the Infura network and your private key. Then, use Hardhat Ignition to deploy your ERC-20 token:

   ```bash
   npx hardhat ignition deploy ./ignition/modules/MyToken.js --network sepolia
   ```

   Make sure your Hardhat configuration (`hardhat.config.js`) includes the correct Sepolia network settings using Infura.

## Contract Verification on Etherscan

Once your contract is deployed, you can verify it on Etherscan to make the source code publicly available.

1. **Install the Hardhat Etherscan Plugin**

   To verify contracts, you’ll need to install the Etherscan plugin:

   ```bash
   npm install --save-dev @nomicfoundation/hardhat-verify
   ```

2. **Update `hardhat.config.js`**

   Add the Etherscan API key to your Hardhat configuration. Get your API key by signing up on [Etherscan](https://etherscan.io/) and navigating to the API key section in your account.

    Set the ETHERSCAN_API_KEY using:
   ```bash
   npx hardhat vars set ETHERSCAN_API_KEY
   ```

3. **Verify the Contract**

   To verify the contract on Sepolia, use the following command, replacing `<contract_address>` with the actual contract address generated during deployment:

   ```bash
   npx hardhat verify --network sepolia <contract_address>
   ```

   This will verify the contract on Etherscan, making it accessible via the blockchain explorer.

## Additional Commands

- To explore more Hardhat functionalities:

  ```bash
  npx hardhat help
  ```

## Key Considerations

- **Security**: Never share your private key or expose it in public repositories.
- **Gas Optimization**: Use gas reporting tools to monitor the cost of your transactions.
- **Testing**: Always test thoroughly on a local or test network before deploying to Ethereum Mainnet.

Further details can be found at [Hardhat's documentation](https://hardhat.org/tutorial/deploying-to-a-live-network).