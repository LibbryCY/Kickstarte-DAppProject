# Kickstarter DApp Project

This project is a decentralized crowdfunding platform built on the Ethereum blockchain. It allows users to create and manage fundraising campaigns in a secure and transparent way. The platform uses smart contracts to handle all campaign-related activities, such as creation, voting, unvoting, campaign closure, and fund claiming.

## Key Features

- **Campaign Creation**: Any user can create a campaign by specifying a funding goal, a beneficiary address, and other campaign details. The campaign is then deployed on the Ethereum blockchain.
  
- **Voting (Contributing)**: Supporters can vote for campaigns by contributing a certain amount of ETH. Every contribution increases the campaign's total balance and adds a vote to the campaign.

- **Unvoting (Withdraw Contributions)**: Supporters can also choose to unvote, i.e., withdraw their ETH contributions from campaigns before they are closed. The funds will be deducted from the campaign's balance.

- **Campaign Closure**: Once a campaign reaches its funding goal, it can be closed. This means that no more contributions can be made, and the beneficiary can claim the funds. If the goal is not reached, the campaign remains open for voting until the goal is met or the campaign is manually closed by the creator.

- **Funds Claiming**: Once a campaign is closed, the beneficiary can claim the funds, which are transferred to their Ethereum address.

## Project Structure

- \`frontend/\`: React-based frontend that interacts with the blockchain, allowing users to interact with campaigns.
- \`backend/\`: A NestJS backend that listens for events from the Ethereum blockchain (using WebSockets) and updates the MongoDB database accordingly.
- \`foundry/\`: Solidity smart contracts developed and tested using the Foundry framework.

## Getting Started

### Prerequisites

Before starting, you need the following tools:

- **Node.js and npm** for backend and frontend dependencies.
- **MongoDB** for storing campaign data.
- **Foundry** for compiling and testing Solidity contracts: \`curl -L https://foundry.paradigm.xyz | bash\`
- **MetaMask** or any other Ethereum wallet for interacting with the DApp.

### Installation Steps

1. **Clone the repository**

   \`\`\`bash
   git clone https://github.com/LibbryCY/Kickstarte-DAppProject.git
   \`\`\`

2. **Backend Setup**

   Navigate to the backend folder, install dependencies, and start the server:

   \`\`\`bash
   cd backend
   npm install
   npm start
   \`\`\`

   The backend will listen for Ethereum events and update the MongoDB database accordingly.

3. **Smart Contracts**

   Navigate to the \`foundry/\` folder and use Foundry to compile, test, and deploy the smart contracts to an Ethereum network:

   \`\`\`bash
   cd ../foundry
   forge build
   forge test
   forge script script/Deploy.s.sol:Deploy --rpc-url <YOUR_RPC_URL> --private-key <YOUR_PRIVATE_KEY> --broadcast
   \`\`\`

4. **Frontend Setup**

   Navigate to the frontend folder, install dependencies, and start the React app:

   \`\`\`bash
   cd ../frontend
   npm install
   npm start
   \`\`\`

   This will open the app in your browser (typically at \`http://localhost:3000\`), where you can interact with campaigns.

## How It Works

### Frontend

The frontend is a React application that interacts with Ethereum smart contracts via Web3.js (or ethers.js). Users can view active campaigns, create new campaigns, vote (contribute), unvote (withdraw), and claim funds after the campaign ends.

### Backend

The backend is built with **NestJS**, a framework for building scalable Node.js applications. The backend listens to Ethereum blockchain events using **Web3.js** or **ethers.js**, particularly for events like `CampaignCreated`, `Voted`, `Unvoted`, `CampaignClosed`, and `FundsClaimed`. 

Upon receiving an event, the backend performs the following actions:

- **Campaign Created**: Adds a new campaign to the MongoDB database.
- **Vote**: Updates the campaign balance and number of votes in the database when a contribution is made.
- **Unvote**: Updates the campaign balance and the number of votes when a contribution is withdrawn.
- **Campaign Closed**: Marks a campaign as closed and prevents further votes.
- **Funds Claimed**: Resets the campaign balance after funds have been claimed by the beneficiary.

### Smart Contracts

The smart contracts, written in Solidity, handle the core logic for campaign management:

1. **Campaign Creation**: Allows users to create new campaigns by specifying a funding goal, beneficiary, and other parameters.
2. **Voting**: Enables users to vote (contribute ETH) to campaigns. Each vote increases the campaign balance.
3. **Unvoting**: Allows users to unvote (withdraw ETH) from campaigns before they are closed.
4. **Closing the Campaign**: Once the campaign reaches the funding goal, it can be closed, and the beneficiary can claim the funds.
5. **Claiming Funds**: Beneficiaries can claim funds after a campaign is closed, which will be transferred to their address.

### Contract Deployment

To deploy the smart contract, you can use Foundry's deployment scripts. Once the contract is deployed to an Ethereum network (e.g., Sepolia or Goerli), the backend will interact with it using Web3 or ethers.js to listen for events and update the database accordingly.

## Usage

1. **Start the frontend application** and connect your wallet (e.g., MetaMask).
2. **Create a campaign** by providing details such as the funding goal, beneficiary address, etc.
3. **Vote for campaigns** by contributing ETH to the campaigns you believe in.
4. **Unvote** if you change your mind and want to withdraw your contribution.
5. **Claim funds** after the campaign has been closed (and the goal has been met).

## License

This project is licensed under the MIT License.
