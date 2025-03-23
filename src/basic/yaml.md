# Using TOML or YAML Config Files


You can set Erigon flags via a YAML or TOML configuration file with the flag `--config`. The flags set in the configuration file can be overridden by writing the flags directly to the Erigon command line.

## YAML

Assuming we have `--chain=mainnet` in our configuration file, adding `--chain=holesky` will override the flag inside the yaml configuration file and set the chain to Holesky.

```bash
./build/bin/erigon --config ./config.yaml --chain=holesky
```

Example of setting up a YAML config file:

```bash
datadir : 'your datadir'
chain : "mainnet"
http : true

http.api : ["eth","debug","net"]
```

## TOML

Example of setting up TOML config file:

```bash
datadir = 'your datadir'
chain = "mainnet"
http = true

"http.api" = ["eth","debug","net"]
```