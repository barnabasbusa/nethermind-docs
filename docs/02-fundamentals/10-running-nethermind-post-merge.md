import Tabs from "@theme/Tabs";
import TabItem from "@theme/TabItem";

# Running Nethermind & CL

## Introduction

Merge

Ethereum’s long awaited shift from Proof of Work (POW) to Proof of Stake (POS) known as The Merge happened on September
15, 2022 and came with fundamental changes to the network. The most notable change is the addition of the Beacon chain (
Consensus layer) which replaced Proof of Work mining. It is coordinating and pseudorandomly selecting block producers
from the pool of stakers / validators in a way that makes it extremely difficult for validators to coordinate attacks on
the network.

The Merge changed how operators run nodes on the Ethereum blockchain. A node now needs **two** clients that work
together as a pair. In addition to the Execution Layer client (e.g. Nethermind) you need a Consensus Layer client that
connects to the Beacon chain and runs the POS algorithm.

This guide will show you everything you need to know to operate an Ethereum node. It will show how to connect to the
Goerli, Sepolia and Chiado test networks as well.

An easy way to run both CL and EL clients is by using [Sedge](https://docs.sedge.nethermind.io). Sedge is a setup tool
for PoS network/chain validators and
nodes. Currently, Sedge supports multiple Linux distributions and MacOS.

To do your setup manually follow the steps below.

## Step 1: Installing Nethermind

You can choose from downloading the official release, downloading the docker image, or building Nethermind from source.

### Downloading Official Release

#### Ubuntu

Run the following commands to enable our launchpad repository run then install Nethermind

```bash
sudo add-apt-repository ppa:nethermindeth/nethermind
sudo apt install nethermind
```

#### macOS

Run the following commands to add the Nethermind repository to your local Homebrew and install

```bash
brew tap nethermindeth/nethermind
brew install nethermind
```

#### Windows

On Windows all you have to do is install and unzip the packages. There are two sources that you can download from.

- [Nethermind Downloads](https://downloads.nethermind.io)
- [Nethermind Github Releases](https://github.com/NethermindEth/nethermind/releases)

### Downloading Docker Image

To download the latest Docker image run the following command to install the latest Debian biased Nethermind image.

```bash
docker pull nethermind/nethermind
```

:::info
Currently Nethermind only supports images for **AMD64** and **ARM64** CPU architectures.
:::

### Building From Source

#### Installing Dependencies

To build Nethermind you will need to have [Git](https://git-scm.com/downloads) and
the [.NET SDK 7.0](https://dotnet.microsoft.com/en-us/download) installed.

Depending on the platform you are using you may need to install extra dependencies.

#### **Windows**

You may need to
install [Microsoft Visual C++ Redistributable](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170)

#### **macOS**

You will need to install the following packages.

```bash
brew install gmp snappy lz4 zstd
```

#### **Ubuntu and Debian**

You will need to install the following packages

```bash
sudo apt-get update && sudo apt-get install libsnappy-dev libc6-dev libc6
```

Commands for other Linux distros can be
found [here](https://docs.nethermind.io/nethermind/ethereum-client/building-nethermind#linux).

#### Building Nethermind

After you have installed all of the dependencies for your platform you need to clone the Nethermind repo from GitHub.

Once the download has finished enter the `nethermind/src/Nethermind` directory and run the build command.

```bash
git clone --recursive https://github.com/NethermindEth/nethermind.git
cd nethermind/src/Nethermind
dotnet build Nethermind.sln -c Release
```

## Step 2: Installing Consensus Client

On the Consensus Layer you have five client implementations to choose from. Though all CL clients are great check them
out for yourself and find the client best suited to your needs.

:::caution
We urge you to take [client diversity](https://clientdiversity.org) into consideration when choosing your CL client and
avoid majority clients.
:::

### Clients

- [Prysm](https://prysmaticlabs.com)
- [Teku](https://consensys.net/knowledge-base/ethereum-2/teku/)
- [Lighthouse](https://lighthouse.sigmaprime.io)
- [Lodestar](https://lodestar.chainsafe.io)
- [Nimbus](https://nimbus.team/#about)

## Step 3 : Configure JSON-RPC API

### JWT Secrets

[JSON Web Token](https://jwt.io) authentication was added to the JSON-RPC API for security reasons to ensure that
nothing interferes with
the communication between the Execution Client (Nethermind in this case) and the Consensus Client. This requires you to
create a file containing a hexadecimal “secret” that will be passed to each .

To create this “Secret File” use the following command.

```bash
openssl rand -hex 32 | tr -d "\n" > "/tmp/jwtsecret"
```

Install [OpenSSL for Windows](https://wiki.openssl.org/index.php/Binaries) then simply type on your Terminal or Command
Prompt (make sure you add the binaries directory to your environment variables or run the terminal from there)
where `"/tmp/jwtsecret"` will be the file path and name when created.

If you do not want to install OpenSSL, you may use a random hex generator website. All you need is a 64 character hex
string saved to a `.txt` file. Example:

```
fcba4ab3138530cf233568bee2d518dd960da77355333d5ac856e1f27487dc9c
```

:::danger
We strongly recommend you to use OpenSSL to generate the secret locally because of security reasons
:::

## Step 4: Run Consensus Client

Ensure you have:

1. Installed Nethermind
2. Installed Consensus client
3. Created a JWT secret file
4. Engine module is enabled with authenticated port - it is a default setting

Then you are ready to start your clients. First start up Consensus Layer.

See section below for commands to run the CL client you installed. You will need to make sure the `--jwt-secret` has the
correct path as well or the clients will not be able to communicate.

Once both clients are running watch the logs to make sure you don't get any `Unauthorized` errors to ensure the clients
are communicating.

:::tip
**Checkpoint Sync**

It would be way faster to sync consensus clients using checkpoint sync.

To sync the CL client using a checkpoint sync, view the community maintained endpoints
[here](https://eth-clients.github.io/checkpoint-sync-endpoints/)

For Goerli or Sepolia see [here](https://notes.ethereum.org/@launchpad/checkpoint-sync).

:::

### Running Nimbus

<Tabs>
<TabItem value="mainnet" label="Mainnet" default>

```bash
nimbus-eth2/build/nimbus_beacon_node \
--network=mainnet \
--web3-url=http://127.0.0.1:8551 \
--rest \
--metrics-explanation \
--suggested-fee-recipient='Enter-eth-address-here' \
--jwt-secret="/tmp/jwtsecret"
```

For checkpoint sync, add the following flag with a checkpoint sync endpoint
Example:

```bash
--trusted-node-url=https://beaconstate.ethstaker.cc
```

</TabItem>
<TabItem value="goerli" label="Goerli">

```bash
nimbus-eth2/build/nimbus_beacon_node \
--network=goerli \
--web3-url=http://127.0.0.1:8551 \
--rest \
--metrics-explanation \
--suggested-fee-recipient='Enter-eth-address-here' \
--jwt-secret="/tmp/jwtsecret"
```

</TabItem>
<TabItem value="sepolia" label="Sepolia">

```bash
nimbus-eth2/build/nimbus_beacon_node \
--network=sepolia \
--web3-url=http://127.0.0.1:8551 \
--rest \
--metrics \
--suggested-fee-recipient='Enter-eth-address-here' \
--jwt-secret="/tmp/jwtsecret"
```

</TabItem>
</Tabs>

### Running Prysm

<Tabs>
<TabItem value="mainnet" label="Mainnet" default>

``` bash
cd prysm
./prysm.sh beacon-chain \
--mainnet \
--datadir "$db_path" \
--suggested-fee-recipient='Enter-eth-address-here' \
--execution-endpoint=http://localhost:8551 \
--jwt-secret="/tmp/jwtsecret"
```

For checkpoint sync, add the following flag with a checkpoint sync endpoint
Example

```bash
--checkpoint-sync-url="https://beaconstate.ethstaker.cc"
--genesis-beacon-api-url="https://beaconstate.ethstaker.cc"
```

</TabItem>
<TabItem value="goerli" label="Goerli">

``` bash
cd prysm
./prysm.sh beacon-chain \
--goerli \
--datadir $db_path \
--suggested-fee-recipient='Enter-eth-address-here' \
--execution-endpoint=http://localhost:8551 \
--jwt-secret=/tmp/jwtsecret
```

</TabItem>
<TabItem value="sepolia" label="Sepolia">

```bash
cd prysm
./prysm.sh beacon-chain \
--sepolia \
--datadir $db_path \
--suggested-fee-recipient='Enter-eth-address-here' \
--execution-endpoint=http://localhost:8551 \
--jwt-secret=/tmp/jwtsecret
```

</TabItem>
<TabItem value="chiado" label="Chiado">

Please follow guide provided [here](https://github.com/gnosischain/prysm-client).
</TabItem>

</Tabs>

### Running Lighthouse

<Tabs>
<TabItem value="mainnet" label="Mainnet">

```bash
lighthouse \
beacon_node \
--network mainnet \
--debug-level info \
--datadir ./mainnet-lh1 \
--eth1 \
--http \
--http-allow-sync-stalled \
--metrics-explanation \
--execution-endpoints http://127.0.0.1:8551 \
--enr-udp-port=9000 \
--enr-tcp-port=9000 \
--discovery-port=9000 \
--suggested-fee-recipient=
'Enter-eth-address-here' \
--jwt-secrets="/tmp/jwtsecret"
```

For checkpoint sync, add the following flag with a checkpoint sync endpoint
Example:

```bash
--checkpoint-sync-url "https://beaconstate.ethstaker.cc"
```

</TabItem>
<TabItem value="goerli" label="Goerli">

```bash
lighthouse \
beacon_node \
--network goerli \
--debug-level info \
--datadir ./testnet-lh1 \
--eth1 \
--http \
--http-allow-sync-stalled \
--metrics-explanation \
--execution-endpoints http://127.0.0.1:8551 \
--enr-udp-port=9000 \
--enr-tcp-port=9000 \
--discovery-port=9000 \
--suggested-fee-recipient=
'Enter-eth-address-here' \
--jwt-secrets="/tmp/jwtsecret"
```

</TabItem>
<TabItem value="sepolia" label="Sepolia">

```bash
lighthouse \
beacon_node \
--network sepolia \
--debug-level info \
--datadir ./testnet-lh1 \
--eth1 \
--http \
--http-allow-sync-stalled \
--metrics \
--execution-endpoints http://127.0.0.1:8551 \
--enr-udp-port=9000 \
--enr-tcp-port=9000 \
--discovery-port=9000 \
--suggested-fee-recipient=
'Enter-eth-address-here' \
--jwt-secrets="/tmp/jwtsecret"
```

</TabItem>
<TabItem value="chiado" label="Chiado">

Please follow guide provided [here](https://github.com/gnosischain/lighthouse-client).
</TabItem>

</Tabs>

### Running Lodestar

<Tabs>
<TabItem value="mainnet" label="Mainnet">

```bash
cd lodestar
./lodestar beacon \
--dataDir "../lodestar-beacondata" \
--network mainnet \
--eth1 \
--execution.urls "http://127.0.0.1:8551" \
--discv5 \
--suggestedFeeRecipient 'Enter-eth-address-here' \
--jwt-secret "/tmp/jwtsecret"

```

For checkpoint sync, add the following flag with a checkpoint sync endpoint
Example:

```bash
--checkpointSyncUrl "https://beaconstate.ethstaker.cc"
```

</TabItem>
<TabItem value="goerli" label="Goerli">

```bash
cd lodestar
./lodestar beacon \
--dataDir "../lodestar-beacondata" \
--network goerli \
--eth1 \
--execution.urls "http://127.0.0.1:8551" \
--discv5 \
--suggestedFeeRecipient 'Enter-eth-address-here' \
--jwt-secret "/tmp/jwtsecret"
```

</TabItem>
<TabItem value="sepolia" label="Sepolia">

```bash
cd lodestar
./lodestar beacon \
--dataDir "../lodestar-beacondata" \
--network sepolia \
--eth1 \
--execution.urls "http://127.0.0.1:8551" \
--discv5 \
--suggestedFeeRecipient 'Enter-eth-address-here' \
--jwt-secret "/tmp/jwtsecret"
```

</TabItem>
<TabItem value="chiado" label="Chiado">

Please follow guide provided [here](https://github.com/gnosischain/lodestar-client).
</TabItem>

</Tabs>

### Running Teku

<Tabs>
<TabItem value="mainnet" label="Mainnet">

```bash
./teku/build/install/teku/bin/teku \
--data-path "datadir-teku" \
--network mainnet \
--ee-endpoint http://localhost:8551 \
--ee-jwt-secret-file "/tmp/jwtsecret" \
--log-destination console \
```

For checkpoint sync, add the following flag with a checkpoint sync endpoint
Example:

```bash
--initial-state="https://beaconstate.ethstaker.cc"
```

</TabItem>
<TabItem value="goerli" label="Goerli">

```bash
./teku/build/install/teku/bin/teku \
--data-path "datadir-teku" \
--network goerli \
--ee-endpoint http://localhost:8551 \
--ee-jwt-secret-file "/tmp/jwtsecret" \
--log-destination console \
--validators-proposer-default-fee-recipient='Enter-eth-address-here'
```

</TabItem>
<TabItem value="sepolia" label="Sepolia">

``` bash
./teku/build/install/teku/bin/teku \
--data-path "datadir-teku" \
--network sepolia \
--ee-endpoint http://localhost:8551 \
--ee-jwt-secret-file "/tmp/jwtsecret" \
--log-destination console \
--validators-proposer-default-fee-recipient='Enter-eth-address-here'
```

</TabItem>
<TabItem value="chiado" label="Chiado">

Please follow guide provided [here](https://github.com/gnosischain/teku-client).
</TabItem>

</Tabs>

## Step 5: Run Nethermind

Once Consensus Layer has started you can start Nethermind client.&#x20;

:::danger
Since the Ethereum merge, you are required to set the Merge.Enabled=true flag. This is not required if you are
using
the
default config files as this is enabled by default.
:::

### Choosing the Network

Depending on the network you want to run the node for, choose the `--config` variable. For more about networks,
check [here](../get-started/networks.md).

`--config` is the config file for the network you want to connect to. For example, to run a node for the goerli
testnet use `--config goerli`.

### Running Local Build

After you have built Nethermind you should be in the `nethermind/src/Nethermind` directory. From there you will need to
run the following commands.

```bash
cd Nethermind.Runner
dotnet run -c Release --config mainnet --JsonRpc.JwtSecretFile=PATH
```

Where PATH is the path to your JWT secret. ex `--JsonRpc.JwtSecretFile=/tmp/jwtsecret`

### Running Release

You have two options when running from a release. The `Nethermind.Launcher` which is a simple GUI with options
to
configure your node, or the `Nethermind.Runner` where you can configure your node by hand.

You will need to be in the directory that the `Nethermind.Runner` and `Nethermind.Launcher` are in to run
Nethermind.

#### Nethermind.Launcher

<Tabs>
<TabItem value="windows" label="Windows">

```bash
./Nethermind.Launcher
````

</TabItem>
<TabItem value="ubuntu" label="Ubuntu">

```bash
nethermind

```

</TabItem>
<TabItem value="macOS" label="macOS">

```bash
nethermind-launcher
```

</TabItem>
</Tabs>

#### Nethermind.Runner

<Tabs>
<TabItem value="windows" label="Windows">

```bash 
./Nethermind.Runner --config goerli --JsonRpc.JwtSecretFile=PATH 
```

</TabItem>
<TabItem value="ubuntu" label="Ubuntu">

```bash
nethermind --config goerli --JsonRpc.JwtSecretFile=PATH 
```

</TabItem>
<TabItem value="macOS" label="macOS">

```bash 
nethermind --config goerli --JsonRpc.JwtSecretFile=PATH 
```

</TabItem>
</Tabs>

:::info
`--config` flag is the network. for example it can be mainnet, goerli or sepolia.
:::

Where PATH is the path to your JWT secret. ex `--JsonRpc.JwtSecretFile=/tmp/jwtsecret`

:::danger
If you are not using the default config files, make sure you also use the **Merge.Enabled=true** flag when launching the
client.
:::

### Running Docker Image

Running Nethermind from a Docker image may require more configuration. The commands below should work in most
situations

```bash
docker run -it -v /home/user/data:/nethermind/data nethermind/nethermind --config goerli --JsonRpc.Enabled true
--JsonRpc.JwtSecretFile=PATH --datadir data
```

:::info
`--config` flag is the network. For example it can be mainnet, goerli or sepolia. **If you are not using the
config file, make sure you set Merge.Enabled=true as flag.**
:::

#### Docker Settings

- `-v /home/user/data:/nethermind/data` sets local directory we will be storing our data to

On some OS like Amazon Linux you may need to increase the `nofile` limit by adding the following instruction to
docker
command `-ulimit nofile=1000000:1000000` or you can take a look
an [alternative
solution](https://stackoverflow.com/questions/62127643/need-understand-ulimits-nofile-setting-in-host-and-container/62136351#62136351).

#### Nethermind Settings

- `--JsonRpc.JwtSecretFile=PATH` where PATH is the location of your JWT secret ex. `/tmp/jwtsecret`
- `--datadir data` maps the database, keystore, and logs all at once