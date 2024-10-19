# Block production

How to propose and validate blockswith Erigon

Only remote miners are supported.

    To enable, add --mine --miner.etherbase=... or --mine --miner.miner.sigkey=... flags.

    Other supported options: --miner.extradata, --miner.notify, --miner.gaslimit, --miner.gasprice , --miner.gastarget

    JSON-RPC supports methods: eth_coinbase , eth_hashrate, eth_mining, eth_getWork, eth_submitWork, eth_submitHashrate

    JSON-RPC supports websocket methods: newPendingTransaction

More info here.
Using Caplin as validator

Only Lighthouse, Lodestar and Teku are supported as Validator Clients.

To enable block production and Caplin's beacon API when using Caplin as the Consensus Layer (CL) engine, the flag --beacon.api must be added. For example:

--beacon.api=beacon,builder,config,debug,node,validator,lighthouse

Enabling the Beacon API will lead to a 6 GB higher RAM usage.

For example, if you want to run Erigon + Caplin as a validator here following is the Erigon command:

./build/bin/erigon --internalcl --chain=holesky --prune=hrtc --beacon.api=beacon,builder,config,debug,node,validator,lighthouse

While here the command for Lighthouse would look like*:

lighthouse validator_client --network holesky --beacon-nodes http://localhost:5555

*For adding validators and specific command syntax, refer to the documentation of your chosen Validator Client.