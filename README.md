# Arbitrum's Orbit Roll Up Chain
chain name: WolfWorldRunChain^_^<3
chain id: 42042042069
-----------------------------------------------------------------------------------

Here I am launching my first chain with Arbitrum's Orbit rollup. I used https://github.com/OffchainLabs/orbit-setup-script to deploy WolfWorldRunChain locally within a docker container. The instructions were simple to follow. Preceeding my local chain deployment I deployed my chain's base contract to Arbitrum Sepolia using the QuickStart (https://docs.arbitrum.io/launch-orbit-chain/orbit-quickstart). 

# What happened?

- I sent a deployment transaction to an Orbit factory smart contract (smart contract designed to deploy other smart contracts) on the Arbitrum testnet. This is the public L2 chain that WolfWorldRunChain^_^<3 will settle transactions to.
- The factory smart contract intiialized my WolfWorldRunChain^_^<3 base contract with the values I set and deployed to Arbitrum testnet. WolfWorldRunChain^_^<3 base contracts are responsible for facilitating the exchance of information between base chain nodes and my local run WolfWorldRunChain^_^<3 nodes. This includes batch posting of transactions to Arbitrum testnet, token staking by WolfWorldRunChain^_^<3 validators, briding mechanism and more.
- Ran the docker instance from the root of the orbit-setup-script repository including my own config files.
- A Nitro node and BlockScout explorer instance is started.  http://localhost/ to access BlockScout explorer instance - this will allow me to view WolfWorldRunChain^_^<3 transactions and blocks, which can be useful for debugging.
- Ran provided hardhat script with private key of owner account to deploys my chains contracts. This handles the following: 
  - Fund the batch-poster and validator (staker) accounts on your underlying L2 chain.
  - Deposit ETH into your account on the chain using your chain's newly deployed bridge.
  - Deploy your Token Bridge contracts on both L2 and local Orbit chains.
  - Configure parameters on the chain.



# orbit-setup-script

These scripts will help you fund newly generated batch-poster and validator addresses, configure an Orbit chain, and deploy bridge contracts on both L2 and L3 chains.

## Instructions

Once you’ve downloaded both config files from the [Orbit Deployment UI](https://orbit.arbitrum.io/), please follow the steps below to complete local deployment of your Orbit chain. For more details and step-by-step instructions, check out the [documentation](https://developer.arbitrum.io/launch-orbit-chain/orbit-quickstart).

1. Clone the https://github.com/OffchainLabs/orbit-setup-script repository, and run `yarn install`. Then, move both the `nodeConfig.json` and `orbitSetupScriptConfig.json` files into the `config` directory within the cloned repository
2. Launch Docker, and in the base directory, run `docker-compose up -d`. This will launch the node with a public RPC reachable at http://localhost:8449/  and a corresponding BlockScout explorer instance, viewable at http://localhost/
3. Then, add the private key for the wallet you used to deploy the rollup contracts earlier in the following command, and run it: `PRIVATE_KEY="0xYourPrivateKey" L2_RPC_URL="<https://sepolia-rollup.arbitrum.io/rpc>" L3_RPC_URL="http://localhost:8449" yarn run setup`
4. The Orbit chain is now up. You can find all information about the newly deployed chain in the `outputInfo.json` file which is created in the main directory of script folder
5. Optionally, to track logs, run the following command within the base directory: `docker-compose logs -f nitro`
