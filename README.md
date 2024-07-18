# Arbitrum's Orbit Roll Up Chain
name: WolfWorldRunChain^_^<3
chain id: 42042042069

# WolfWorldRun Token address: 
0xb83293bcb10f0c8ce1171fabb398277cd4ae1019

# EtherScan URL: 
https://sepolia.etherscan.io/tx/0x37b9d90a3292ad1d6a69d6a135474499d48022f4d011916701e7a612a4710a88 

# Deploy Locally:
https://orbit.arbitrum.io/deployment/step/deploy-local

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



