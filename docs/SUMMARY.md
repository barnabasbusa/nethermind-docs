# Table of contents

* [Welcome to Nethermind](README.md)

## First steps with Nethermind

* [Running Nethermind & CL](first-steps-with-nethermind/running-nethermind-post-merge.md)
* [System Requirements](first-steps-with-nethermind/system-requirements.md)
* [Firewall Configuration](first-steps-with-nethermind/firewall-configuration.md)
* [Migrating From Geth](first-steps-with-nethermind/migrating-from-geth.md)
* [Explaining Nethermind logs](first-steps-with-nethermind/getting-started.md)
* [Security](first-steps-with-nethermind/security.md)
* [Manage Nethermind with systemd](first-steps-with-nethermind/manage-nethermind-with-systemd.md)
* [Connecting Wallet](first-steps-with-nethermind/connecting-wallet.md)

## Nodes and The Merge

* [The Merge](nodes-and-the-merge/the-merge.md)
* [Nethermind Changes](nodes-and-the-merge/nethermind-changes.md)
* [Troubleshooting Issues](nodes-and-the-merge/troubleshooting-issues/README.md)
  * [Missing Attestations](nodes-and-the-merge/troubleshooting-issues/missing-attestations.md)

## Installing Nethermind

* [Downloading Releases](installing-nethermind/download-sources/README.md)
  * [Downloads Page](http://downloads.nethermind.io)
  * [Github Release Page](https://github.com/NethermindEth/nethermind/releases)
* [Docker](installing-nethermind/docker.md)
* [Launching Nethermind via Nethermind.Launcher](installing-nethermind/launching-nethermind-via-nethermind.launcher.md)

## For developers

* [Building From Source](for-developers/building-nethermind.md)
* [Coding Style](for-developers/coding-style.md)
* [Plugins](for-developers/plugins.md)
* [Web3.py](for-developers/web3.py.md)
* [Custom Analytic Tools](for-developers/custom-analytic-tools.md)

## Ethereum client

* [Running Nethermind](ethereum-client/running-nethermind/README.md)
  * [Running the client](ethereum-client/running-nethermind/running-the-client.md)
  * [Runtime](ethereum-client/running-nethermind/runtime.md)
* [Sync modes](ethereum-client/sync-modes.md)
* [JSON RPC](ethereum-client/json-rpc/README.md)
  * [Engine JsonRpc Config Example](ethereum-client/json-rpc/engine-jsonrpc-config-example.md)
  * [Admin module](ethereum-client/json-rpc/admin.md)
  * [Clique module](ethereum-client/json-rpc/clique.md)
  * [Debug module](ethereum-client/json-rpc/debug.md)
  * [Eth module](ethereum-client/json-rpc/eth.md)
  * [Net module](ethereum-client/json-rpc/net.md)
  * [Parity module](ethereum-client/json-rpc/parity.md)
  * [Personal module](ethereum-client/json-rpc/personal.md)
  * [Proof module](ethereum-client/json-rpc/proof.md)
  * [Subscribe module](ethereum-client/json-rpc/subscribe.md)
  * [Trace module](ethereum-client/json-rpc/trace.md)
  * [TxPool module](ethereum-client/json-rpc/txpool.md)
  * [Web3 module](ethereum-client/json-rpc/web3.md)
  * [JSON RPC WIKI](https://eth.wiki/json-rpc/API)
* [Using Docker](ethereum-client/docker.md)
* [Networks](ethereum-client/networks.md)
* [Private Networks](ethereum-client/private-networks/README.md)
  * [How to setup a Nethermind only Clique based chain](ethereum-client/private-networks/how-to-setup-a-nethermind-only-clique-based-chain.md)
  * [How to setup a Nethermind only Spaceneth based chain](ethereum-client/private-networks/how-to-setup-a-nethermind-only-spaceneth-based-chain.md)
* [Database](ethereum-client/database.md)
* [Metrics](ethereum-client/metrics-explanation/README.md)
  * [Using dotnet-counters](ethereum-client/metrics-explanation/dotnet-counters.md)
  * [Using Prometheus and Grafana](ethereum-client/metrics-explanation/setting-up-local-metrics-infrastracture.md)
  * [Aura module](ethereum-client/metrics-explanation/consensus.aura.md)
  * [Blockchain module](ethereum-client/metrics-explanation/blockchain.md)
  * [Evm module](ethereum-client/metrics-explanation/evm.md)
  * [JsonRpc module](ethereum-client/metrics-explanation/jsonrpc.md)
  * [Merge module](ethereum-client/metrics-explanation/merge.plugin.md)
  * [Network module](ethereum-client/metrics-explanation/network.md)
  * [Pruning module](ethereum-client/metrics-explanation/trie.pruning.md)
  * [Runner module](ethereum-client/metrics-explanation/runner.md)
  * [Store module](ethereum-client/metrics-explanation/store.md)
  * [Trie module](ethereum-client/metrics-explanation/trie.md)
  * [TxPool module](ethereum-client/metrics-explanation/txpool.md)
* [Logging Configuration](ethereum-client/logging-configuration.md)
* [Configuration](ethereum-client/configuration/README.md)
  * [Sample configuration](ethereum-client/configuration/sample-configuration.md)
  * [Aura module](ethereum-client/configuration/aura.md)
  * [Blocks module](ethereum-client/configuration/blocks.md)
  * [Bloom module](ethereum-client/configuration/bloom.md)
  * [EthStats module](ethereum-client/configuration/ethstats.md)
  * [HealthChecks module](ethereum-client/configuration/healthchecks.md)
  * [Hive module](ethereum-client/configuration/hive.md)
  * [Init module](ethereum-client/configuration/init.md)
  * [JsonRpc module](ethereum-client/configuration/jsonrpc.md)
  * [Keystore module](ethereum-client/configuration/keystore.md)
  * [Merge module](ethereum-client/configuration/merge.md)
  * [Metrics module](ethereum-client/configuration/metrics.md)
  * [Mining module](ethereum-client/configuration/mining.md)
  * [Network module](ethereum-client/configuration/network.md)
  * [Pruning module](ethereum-client/configuration/pruning.md)
  * [Receipt module](ethereum-client/configuration/receipt.md)
  * [Seq module](ethereum-client/configuration/seq.md)
  * [Sync module](ethereum-client/configuration/sync.md)
  * [TxPool module](ethereum-client/configuration/txpool.md)
  * [Wallet module](ethereum-client/configuration/wallet.md)
* [Monitoring Node's Health](ethereum-client/monitoring-node-health.md)

## Nethermind utilities

* [CLI](nethermind-utilities/cli/README.md)
  * [Admin module](nethermind-utilities/cli/admin.md)
  * [Clique module](nethermind-utilities/cli/clique.md)
  * [Debug module](nethermind-utilities/cli/debug.md)
  * [Diag module](nethermind-utilities/cli/diag.md)
  * [Eth module](nethermind-utilities/cli/eth.md)
  * [Net module](nethermind-utilities/cli/net.md)
  * [Node module](nethermind-utilities/cli/node.md)
  * [Parity module](nethermind-utilities/cli/parity.md)
  * [Personal module](nethermind-utilities/cli/personal.md)
  * [Proof module](nethermind-utilities/cli/proof.md)
  * [System module](nethermind-utilities/cli/system.md)
  * [Trace module](nethermind-utilities/cli/trace.md)
  * [TxPool module](nethermind-utilities/cli/txpool.md)
  * [Web3 module](nethermind-utilities/cli/web3.md)

## Guides and Helpers

* [FAQ](guides-and-helpers/faq.md)
* [Deploy Nethermind with Monitoring stack](guides-and-helpers/deploy-nethermind-with-monitoring-stack.md)
* [Known Issues](guides-and-helpers/known-issues/README.md)
  * [ETH2 issues](guides-and-helpers/known-issues/eth2-issues.md)
* [Validator setup](guides-and-helpers/validator-setup/README.md)
  * [Aura Validator](guides-and-helpers/validator-setup/aura-validator.md)
  * [Eth2 Validator](guides-and-helpers/validator-setup/eth2-validator.md)
* [ETH2 <-> Nethermind](guides-and-helpers/eth2-less-than-greater-than-nethermind.md)
* [How to reduce database size](guides-and-helpers/how-to-reduce-database-size/README.md)
  * [Resync database from scratch](guides-and-helpers/how-to-reduce-database-size/resync-database-from-scratch.md)
  * [Full Pruning](guides-and-helpers/how-to-reduce-database-size/full-pruning.md)

## Contact

* [Social Media](contact/social-media.md)
* [Contact us](contact/contact-us.md)