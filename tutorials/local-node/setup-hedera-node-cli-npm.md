# Set Up a Hedera Local Node Using the `hedera-local` CLI

This tutorial demonstrates how to set up and run a Hedera node locally using the [@hashgraph/hedera-local](https://www.npmjs.com/package/@hashgraph/hedera-local) command line interface (CLI) tool. This tool includes the necessary definitions for Docker Compose and abstracts away the need to interact directly with Docker when running your node. This is the recommended method for standing up a local node, but you can also run a local node [manually with Docker](https://www.youtube.com/watch?v=KOhzu6ftmbY) or [in a cloud development environment](https://docs.hedera.com/hedera/tutorials/local-node/how-to-run-hedera-local-node-in-a-cloud-development-environment-cde) (CDE).

## Requirements

Before continuing, ensure that you have the following software installed:

* [Node.js](https://nodejs.org/) >= v14.x (Check version: `node -v`)
* [npm](https://www.npmjs.com/) >= v6.14.17 (Check version: `npm -v`)
* [Docker](https://www.docker.com/) >= v20.10.x (Check version: `docker -v`)
* [Docker Compose](https://docs.docker.com/compose/) >= v2.12.3 (Check version: `docker compose version`)

Hardware requirements: minimum 16 GB RAM

## Getting Started

### Configure Docker

The `hedera-local` tool uses Docker behind the scenes, so you'll need to configure Docker according to the following specifications to run a local node.

Open Docker and navigate to **Settings > General**. Make sure that the **VirtioFS** file sharing implementation is selected.

In **Settings > Resources**, ensure the following minimum resources are available:

  - **CPUs:** 6
  - **Memory:** 8 GB
  - **Swap:** 1 GB
  - **Disk Image Size:** 64 GB

In **Settings > Advanced**, make sure that **Allow the default Docker sockets to be used (requires password)** is checked.

### Install the `hedera-local` CLI Tool

To run a local node using the `hedera-local` CLI tool, you can either install it globally via npm, or else run it locally from a clone of [the `hedera-local-node` GitHub repo](https://github.com/hashgraph/hedera-local-node). The [global npm installation](#global-npm-installation) is generally recommended for most users unless you specifically need to test the latest changes to the repo, in which case you should follow the [local development installation](#local-development-installation) instructions.

#### Global npm Installation

Run the following command to install the `@hashgraph/hedera-local` CLI tool globally:

```bash
npm install @hashgraph/hedera-local -g
```

Now you can use [the `hedera` commands](#hedera-commands) from any starting place in your terminal when [running your node](#running-the-node).

#### Local Development Installation

Clone the `hedera-local-node` repo and navigate to the project directory:

```bash
git clone https://github.com/hashgraph/hedera-local-node.git 
cd hedera-local-node
```

Install the necessary dependencies in the `hedera-local-node` directory:

```bash
npm install && npm install -g
```

Now you can use `npm run start`, `npm run stop`, and `npm run restart` within the project directory to start, stop, and restart the node, respectively.

## Running the Node

Note: This section assumes you've [installed `hedera-local` globally](#global-npm-installation). If you're running it from a local repo, you must replace `hedera *` with `npm run *` and add `--` before any optional flags. For example, `hedera start -d` would be `npm run start -- -d`.

### `hedera` Commands

Run `hedera` in your terminal to see the list of commonly used commands and options:

```bash
$ hedera
hedera <command>

Commands:
  hedera start [accounts]              Starts the local hedera network.
  hedera stop                          Stops the local hedera network and delete
                                       all the existing data.
  hedera restart [accounts]            Restart the local hedera network.
  hedera generate-accounts [accounts]  Generates the specified number of
                                       accounts [default: 10]
  hedera debug [timestamp]             Parses and prints the contents of the
                                       record file that has been created during
                                       the selected timestamp.

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]
```

See [the project readme](https://github.com/hashgraph/hedera-local-node) for a complete list of options and flags, which are beyond the scope of this introductory tutorial.

#### Start the Node

Run `hedera start` to start the local node.

You should see the following response in the terminal:

```bash
[Hedera-Local-Node] INFO (StateController) [✔︎] Starting start procedure!
[Hedera-Local-Node] INFO (InitState) ⏳ Making sure that Docker is started and it is correct version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker compose version...
[Hedera-Local-Node] INFO (DockerService) ⏳ Checking docker resources...
[Hedera-Local-Node] INFO (InitState) ⏳ Setting configuration with latest images on host 127.0.0.1 with dev mode turned off using turbo mode in single node configuration...
[Hedera-Local-Node] INFO (InitState) [✔︎] Local Node Working directory set to /Users/sycamore/Library/Application Support/hedera-local.
[Hedera-Local-Node] INFO (InitState) [✔︎] Hedera JSON-RPC Relay rate limits were disabled.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed environment variables were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed mirror node properties were set for this configuration.
[Hedera-Local-Node] INFO (StartState) ⏳ Starting Hedera Local Node...

```

#### Stop the Node

Run `hedera stop` to stop the local node.

You should see the following response in the terminal:

```bash
$ hedera stop
[Hedera-Local-Node] INFO (StateController) [✔︎] Starting stop procedure!
[Hedera-Local-Node] INFO (StopState) ⏳ Initiating stop procedure. Trying to stop docker containers and clean up volumes...
[Hedera-Local-Node] INFO (StopState) ⏳ Stopping the network...
[Hedera-Local-Node] INFO (StopState) [✔︎] Hedera Local Node was stopped successfully.
```

#### Restart the Node

Run `hedera restart` to restart the local node.

You should see the following response in the terminal:

```bash
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
[Hedera-Local-Node] INFO (InitState) ⏳ Setting configuration with latest images on host 127.0.0.1 with dev mode turned off using turbo mode in single node configuration...
[Hedera-Local-Node] INFO (InitState) [✔︎] Local Node Working directory set to /Users/sycamore/Library/Application Support/hedera-local.
[Hedera-Local-Node] INFO (InitState) [✔︎] Hedera JSON-RPC Relay rate limits were disabled.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed environment variables were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed bootsrap properties were set for this configuration.
[Hedera-Local-Node] INFO (InitState) [✔︎] Needed mirror node properties were set for this configuration.
[Hedera-Local-Node] INFO (StartState) ⏳ Starting Hedera Local Node...
```

### Verify Local Node is Running

To verify that your node is running, visit the local mirror node explorer endpoint at [http://localhost:8080/](http://localhost:8080/) in your browser. Select **Localnet** from the dropdown menu to see the Hedera network transactions on your local device. You can click on any of the transactions to view details such as consensus, block, and transaction hash.

![Hedera Explorer - View LOCALNET](../../.gitbook/assets/02-hedera-local-node-terminal-view-localnet.png)

![Hedera Explorer - View LOCALNET Details](../../.gitbook/assets/03-hedera-local-node-terminal-view-localnet-details.png)

#### Send cURL Request to Testnet

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

```bash
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

This error commonly occurs when you already have a local node running—for example, if you've forgotten to stop a local node before starting a new one.

To resolve this error, terminate any existing local node Docker processes as well as any other processes bound to these port numbers before attempting to run the node. You can accomplish this by running `docker compose down -v`, `git clean -xfd`, and `git reset --hard`.

Alternatively, instead of starting a new instance of the network, you can use the `hedera generate-accounts` command to generate new accounts for the network that's already running.

## Next Steps

With your local node up and running, you're now ready to learn how to [deploy a smart contract using Hardhat and Hedera JSON-RPC relay](https://docs.hedera.com/hedera/tutorials/smart-contracts/deploy-a-smart-contract-using-hardhat-hedera-json-rpc-relay).

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><p>Writer: Owanate, Technical Writer</p><p><a href="https://github.com/owans">GitHub</a> | <a href="https://medium.com/@owanateamachree">Medium</a></p></td><td><a href="https://medium.com/@owanateamachree">https://medium.com/@owanateamachree</a></td></tr><tr><td align="center"><p>Editor: Krystal, Technical Writer</p><p><a href="https://github.com/theekrystallee">GitHub</a> | <a href="https://twitter.com/theekrystallee">Twitter</a></p></td><td><a href="https://twitter.com/theekrystallee">https://twitter.com/theekrystallee</a></td></tr></tbody></table>
