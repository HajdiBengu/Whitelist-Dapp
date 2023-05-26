## Whitelist Dapp

This project is a Whitelist Dapp. It gives early supporters access to a whitelist for an NFT collection named “Crypto Devs”. Whitelist access is given to the first 10 users for free who want to get in. The project is simple enough, so it is written mostly in Javascript. The code is split into two parts, the Hardhat project containing the smart contract and the deployment script, and the decentralized app written in Next.js

### Hardhat

If you want to deploy your own smart contract, after cloning the code to your local machine, you will want to add a .env file and populate it with the following lines:

```plaintext
QUICKNODE_HTTP_URL="add-quicknode-http-provider-url-here"
PRIVATE_KEY="add-the-private-key-here"
```

Quicknode is a node provider that lets you connect to various different blockchains. We will be using it to deploy our contract through Hardhat. After creating an account, Create an endpoint on Quicknode, select Ethereum, and then select the Goerli network. Click Continue in the bottom right and then click on Create Endpoint. Copy the link given to you in HTTP Provider and add it to the .env file below for QUICKNODE\_HTTP\_URL.

Also, to get your private key, you need to export it from Metamask. Open Metamask, click on the three dots, click on Account Details and then Export Private Key. MAKE SURE YOU ARE USING A TEST ACCOUNT THAT DOES NOT HAVE MAINNET FUNDS FOR THIS. Add this Private Key below in your .env file for PRIVATE\_KEY variable.

Compile the contract, open up a terminal pointing at hardhat-tutorial directory and execute this command

```plaintext
npx hardhat compile
```

To deploy, open up a terminal pointing at hardhat-tutorial directory and execute this command

```plaintext
npx hardhat run scripts/deploy.js --network goerli
```

The terminal will return the smart contract address.

### Next.js

The website is developed in Next.js and React. If you want to run the app locally and integrate your own deployed whitelist smart contract, you need to go to 

`my-app/constants/index.js`, which should have a structure like this:

```plaintext
export const WHITELIST_CONTRACT_ADDRESS = "YOUR_WHITELIST_CONTRACT_ADDRESS";
export const abi = YOUR_ABI;
```

and replace replace `"YOUR_WHITELIST_CONTRACT_ADDRESS"` with the address of the whitelist contract that you deployed. If the structure of the smart contract is different from the one in the hardhat project, you need to replace `YOUR_ABI` as well. To get the ABI for your contract, go to your `hardhat-tutorial/artifacts/contracts/Whitelist.sol` folder and from your `Whitelist.json` file get the array marked under the `"abi"` key.

Now in your terminal which is pointing to `my-app` folder, execute:

```plaintext
npm run dev
```

The whitelist dapp should be working.
