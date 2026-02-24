# Arbitrum's Layer 3 Blockchain Using Orbit Rollup

**Chain Name:** [redacted]  
**Chain ID:** [redacted]

---

## Overview

This repo documents the deployment of [redacted], an L3 chain built on Arbitrum's Orbit rollup stack. The local chain was deployed using the [orbit-setup-script](https://github.com/OffchainLabs/orbit-setup-script) inside a Docker container, with the base contracts deployed to Arbitrum Sepolia (L2 test net) via the [Orbit QuickStart](https://docs.arbitrum.io/launch-orbit-chain/orbit-quickstart).

---

## What Happened

1. **Factory contract deployment** — A deployment transaction was sent to an Orbit factory smart contract on the Arbitrum Sepolia testnet (the L2 that settles transactions for L3).

2. **Base contract initialization** — The factory contract initialized and deployed my L3's base contracts with custom configuration values. These base contracts handle communication between L2 and L3 nodes, including transaction batch posting, validator staking, and the bridging mechanism.

3. **Docker startup** — The Docker instance was launched from the root of the `orbit-setup-script` repository using custom config files. This starts a Nitro node and a BlockScout explorer instance accessible at `http://localhost/`, useful for viewing transactions and blocks during debugging.

4. **Hardhat setup script** — A provided Hardhat script was run with the owner account's private key. This script handles:
   - Funding the batch-poster and validator (staker) accounts on Arbitrum Sepolia
   - Depositing ETH into the L3 account via the newly deployed bridge
   - Deploying Token Bridge contracts on both the L2 and L3
   - Configuring chain parameters

---

## orbit-setup-script

These scripts fund newly generated batch-poster and validator addresses, configure the Orbit chain, and deploy bridge contracts on both L2 and L3.

### Setup Instructions

1. Clone the [orbit-setup-script](https://github.com/OffchainLabs/orbit-setup-script) repository and install dependencies:
   ```bash
   yarn install
   ```
   Then move both `nodeConfig.json` and `orbitSetupScriptConfig.json` into the `config` directory.

2. Launch Docker and start the node from the base directory:
   ```bash
   docker-compose up -d
   ```
   This exposes a public RPC at `http://localhost:8449/` and a BlockScout explorer at `http://localhost/`.

3. Run the setup script with your owner wallet's private key:
   ```bash
   PRIVATE_KEY="0xYourPrivateKey" \
   L2_RPC_URL="https://sepolia-rollup.arbitrum.io/rpc" \
   L3_RPC_URL="http://localhost:8449" \
   yarn run setup
   ```

4. Once complete, chain details are saved to `outputInfo.json` in the root of the script folder.

5. Optionally, tail the Nitro node logs:
   ```bash
   docker-compose logs -f nitro
   ```

---

## Resources

- [Orbit QuickStart](https://docs.arbitrum.io/launch-orbit-chain/orbit-quickstart)
- [orbit-setup-script](https://github.com/OffchainLabs/orbit-setup-script)
- [Arbitrum Developer Docs](https://developer.arbitrum.io)
