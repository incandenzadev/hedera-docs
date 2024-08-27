# Set Up a Hedera Local Node using the npm CLI

This tutorial demonstrates how to set up and run a Hedera node locally using the [@hashgraph/hedera-local](https://www.npmjs.com/package/@hashgraph/hedera-local) npm command line interface (CLI) tool. This tool includes the necessary definitions for Docker Compose and abstracts away the need to interact directly with Docker when running your node. This is the recommended method for standing up a local node, but you can also run a local node [manually with Docker](https://www.youtube.com/watch?v=KOhzu6ftmbY) or [in a cloud development environment](https://docs.hedera.com/hedera/tutorials/local-node/how-to-run-hedera-local-node-in-a-cloud-development-environment-cde) (CDE).

## Requirements

Before continuing, ensure that you have the following software installed:

* [Node.js](https://nodejs.org/) >= v14.x (Check version: `node -v`)
* [npm](https://www.npmjs.com/) >= v6.14.17 (Check version: `npm -v`)
* [Docker](https://www.docker.com/) >= v20.10.x (Check version: `docker -v`)
* [Docker Compose](https://docs.docker.com/compose/) >= v2.12.3 (Check version: `docker compose version`)

Hardware requirements: minimum 16 GB RAM

## Getting Started

Clone the `hedera-local-node` repo and navigate to the project directory:

```js
git clone https://github.com/hashgraph/hedera-local-node.git 
cd hedera-local-node
```

### Install the CLI Tool

Install the `@hashgraph/hedera-local` CLI tool globally:

```js
npm install @hashgraph/hedera-local -g
```

> Note that the official npm release may not reflect the most recent changes to the main branch of this repository.

### Install Dependencies

Install the necessary dependencies in the `hedera-local-node` directory:

```js
npm install && npm install -g
```

### Configure Docker

Open Docker and navigate to **Settings > General**. Make sure that the VirtioFS file sharing implementation is selected.

In **Settings > Resources**, ensure the following minimum resources are available:

  - **CPUs:** 6
  - **Memory:** 8 GB
  - **Swap:** 1 GB
  - **Disk Image Size:** 64 GB

In **Settings > Advanced**, make sure that **Allow the default Docker sockets to be used (requires password)** is checked.

## Running the Node

With Docker running on your device, start the local node:

```js
npm run start
```

You should see the following response in the terminal:

```bash
hedera-local-node % npm run start

> @hashgraph/hedera-local@2.26.2 restart
> npm run build && node ./build/index.js restart


> @hashgraph/hedera-local@2.26.2 build
> rimraf ./build && tsc

[Hedera-Local-Node] INFO (StateController) [✔︎] Starting restart procedure!
[Hedera-Local-Node] INFO (CleanUpState) ⏳ Initiating clean up procedure. Trying to revert unneeded changes to files...
[Hedera-Local-Node] INFO (CleanUpState) [✔︎] Clean up of consensus node properties finished.
[Hedera-Local-Node] INFO (CleanUpState) [✔︎] Clean up of mirror node properties finished.
[Hedera-Local-Node] INFO (StopState) ⏳ Initiating stop procedure. Trying to stop docker containers and clean up volumes...
[Hedera-Local-Node] INFO (StopState) ⏳ Stopping the network...
[Hedera-Local-Node] INFO (StopState) [✔︎] Hedera Local Node was stopped successfully.
[Hedera-Local-Node] INFO (InitState) ⏳ Making sure that Docker is started and it is correct version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker compose version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker resources...
[Hedera-Local-Node] WARNING (DockerService) [!] Port 3000 is in use.
[Hedera-Local-Node] INFO (InitState) ⏳ Setting configuration with latest images on host 127.0.0.1 with dev mode turned off using turbo mode in single node configuration...
[Hedera-Local-Node] INFO (InitState) [✔︎] Local Node Working directory set to /Users/owanate/Library/Application Support/hedera-local.
[Hedera-Local-Node] INFO (InitState) [✔︎] Hedera JSON-RPC Relay rate limits were disabled.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed environment variables were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed mirror node properties were set for this configuration.
[Hedera-Local-Node] INFO (StartState) ⏳ Starting Hedera Local Node...
```

### Detached Mode

Append the `-- -d` flag to generate default accounts and start the local node in detached mode:

```js
npm run start -- -d
```

You should see the following response in the terminal:

```bash
hedera-local-node % npm run start -- -d

> @hashgraph/hedera-local@2.26.2 start
> npm run build && node ./build/index.js start -d


> @hashgraph/hedera-local@2.26.2 build
> rimraf ./build && tsc
[Hedera-Local-Node] INFO (StartState) [✔︎] Hedera Local Node successfully started!
[Hedera-Local-Node] INFO (NetworkPrepState) ⏳ Starting Network Preparation State...
[Hedera-Local-Node] INFO (NetworkPrepState) [✔︎] Imported fees successfully!
[Hedera-Local-Node] INFO (NetworkPrepState) [✔︎] Topic was created!
[Hedera-Local-Node] INFO (AccountCreationState) ⏳ Starting Account Creation state in synchronous mode ...
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------| Accounts list (ECDSA keys) |----------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |    id    |                            private key                            |  balance |
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1002 - 0x7f109a9e3b0d8ecfba9cc23a3614433ce0fa7ddcc80f2a8f10b222179a5a80d6 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1003 - 0x6ec1f2e7d126a74a1d2ff9e1c5d90b92378c725e506651ff8bb8616a5c724628 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1004 - 0xb4d7f7e82f61d81c95985771b8abf518f9328d019c36849d4214b5f995d13814 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1005 - 0x941536648ac10d5734973e94df413c17809d6cc5e24cd11e947e685acfbd12ae - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1006 - 0x5829cf333ef66b6bdd34950f096cb24e06ef041c5f63e577b4f3362309125863 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1007 - 0x8fc4bffe2b40b2b7db7fd937736c4575a0925511d7a0a2dfc3274e8c17b41d20 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1008 - 0xb6c10e2baaeba1fa4a8b73644db4f28f4bf0912cceb6e8959f73bb423c33bd84 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1009 - 0xfe8875acb38f684b2025d5472445b8e4745705a9e7adc9b0485a05df790df700 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1010 - 0xbdc6e0a69f2921a78e9af930111334a41d3fab44653c8de0775572c526feea2d - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1011 - 0x3e215c3d2a59626a669ed04ec1700f36c05c9b216e592f58bbfd3d8aa6ea25f9 - 10000 ℏ |
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |--------------------------------------------------------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |------------------------------------------------| Accounts list (Alias ECDSA keys) |--------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |--------------------------------------------------------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) |    id    |               public address               |                             private key                            | balance |
[Hedera-Local-Node] INFO (AccountCreationState) |--------------------------------------------------------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) | 0.0.1012 - 0x67d8d32e9bf1a9968a5ff53b87d777aa8ebbee69 - 0x105d050185ccb907fba04dd92d8de9e32c18305e097ab41dadda21489a211524 - 10000 ℏ |
.....
[Hedera-Local-Node] INFO (AccountCreationState) |-----------------------------------------------------------------------------------------|
[Hedera-Local-Node] INFO (AccountCreationState) [✔︎] Accounts created succefully!
[Hedera-Local-Node] INFO (CleanUpState) ⏳ Initiating clean up procedure. Trying to revert unneeded changes to files...
[Hedera-Local-Node] INFO (CleanUpState) [✔︎] Clean up of consensus node properties finished.
[Hedera-Local-Node] INFO (CleanUpState) [✔︎] Clean up of mirror node properties finished.
```

![Running Hedera Node on Terminal](../../.gitbook/assets/01-hedera-local-node-terminal-npm-cli-running.png)

### Other npm commands

* `npm run restart`: restarts the network
* `npm run stop`: stops the network
* `npm run generate-accounts`: generates new accounts—network must be running

## Verify Local Node is Running

To verify that your node is running, visit the local mirror node explorer endpoint at [http://localhost:8080/](http://localhost:8080/) in your browser. Select **Localnet** from the dropdown menu to see the Hedera network transactions on your local device. You can click on any of the transactions to view details such as consensus, block, and transaction hash.

![Hedera Explorer - View LOCALNET](../../.gitbook/assets/02-hedera-local-node-terminal-view-localnet.png)

![Hedera Explorer - View LOCALNET Details](../../.gitbook/assets/03-hedera-local-node-terminal-view-localnet-details.png)

### Send cURL Request to Testnet

To confirm that you're able to interact with the Hedera Testnet using JSON-RPC, try issuing an `eth_getBlockByNumber` JSON-RPC request.

Run the following command in your terminal:

```bash
  curl http://localhost:7546/ \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{"method":"eth_getBlockByNumber","params":["latest",false],"id":1,"jsonrpc":"2.0"}'
```

You should get the following response:

```bash
curl http://localhost:7546/ \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{"method":"eth_getBlockByNumber","params":["latest",false],"id":1,"jsonrpc":"2.0"}'
{"result":{"timestamp":"0x667c000e","difficulty":"0x0","extraData":"0x","gasLimit":"0xe4e1c0","baseFeePerGas":"0xa54f4c3c00","gasUsed":"0x0","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","miner":"0x0000000000000000000000000000000000000000","mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","receiptsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","size":"0x93d","stateRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","totalDifficulty":"0x0","transactions":[],"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","uncles":[],"withdrawals":[],"withdrawalsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","number":"0x1604","hash":"0xfef0932ffb429840fe765d6d87c77425e2991326ddae6747dcce5c929c69ef38","parentHash":"0xef1ef331626f4f50ba2541d440b45cac51c5d8d6b4c46407a00c15d593c31e96"},"jsonrpc":"2.0","id":1}%    
```

## Troubleshooting

### Necessary Ports in Use

**Error: Node cannot start properly because necessary ports are in use!**

```js
hedera-local-node % npm run start -- -d

> @hashgraph/hedera-local@2.26.2 start
> npm run build && node ./build/index.js start -d


> @hashgraph/hedera-local@2.26.2 build
> rimraf ./build && tsc

[Hedera-Local-Node] INFO (StateController) [✔︎] Starting start procedure!
[Hedera-Local-Node] INFO (InitState) ⏳ Making sure that Docker is started and it is correct version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker compose version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker resources...
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 5551 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 8545 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 5600 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 5433 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 8082 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Port 6379 is in use.
[Hedera-Local-Node] WARNING (DockerService) [!] Port 7546 is in use.
[Hedera-Local-Node] WARNING (DockerService) [!] Port 8080 is in use.
[Hedera-Local-Node] WARNING (DockerService) [!] Port 3000 is in use.
[Hedera-Local-Node] ERROR (DockerService) [✘] [✘] Node cannot start properly because necessary ports are in use!
```

To resolve this error, terminate any existing local node Docker processes as well as any other processes bound to these port numbers before attempting to run the node. You can accomplish this by running `docker compose down -v`, `git clean -xfd`, and `git reset --hard`.

Alternatively, instead of starting a new instance of the network, you can use the `npm run generate-accounts` command to generate new accounts for the network that's already running.

## Next Steps

With your local node up and running, you're now ready to learn how to [deploy a smart contract using Hardhat and Hedera JSON-RPC relay](https://docs.hedera.com/hedera/tutorials/smart-contracts/deploy-a-smart-contract-using-hardhat-hedera-json-rpc-relay).

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><p>Writer: Owanate, Technical Writer</p><p><a href="https://github.com/owans">GitHub</a> | <a href="https://medium.com/@owanateamachree">Medium</a></p></td><td><a href="https://medium.com/@owanateamachree">https://medium.com/@owanateamachree</a></td></tr><tr><td align="center"><p>Editor: Krystal, Technical Writer</p><p><a href="https://github.com/theekrystallee">GitHub</a> | <a href="https://twitter.com/theekrystallee">Twitter</a></p></td><td><a href="https://twitter.com/theekrystallee">https://twitter.com/theekrystallee</a></td></tr></tbody></table>
