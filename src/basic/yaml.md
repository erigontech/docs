# Using TOML or YAML Config Files

You can configure Erigon using a YAML or TOML configuration file by specifying its path with the `--config` flag. 

> Note: flags specified in the configuration file can be overridden by directly setting them in the Erigon command line.

Both in YAML and TOML files boolean operators (`false`, `true`) and strings without spaces can be specified without quotes, while strings with spaces must be included in `""` or `''` quotes.

## YAML

Use the `--config` flag to point at the YAML configuration file.

```bash
./build/bin/erigon --config ./config.yaml --chain=holesky
```

Example of setting up a YAML config file:

```yaml
datadir : 'your datadir'
chain : "mainnet"
http : true
http.api : ["eth","debug","net"]
```

In this case the `--chain` flag in the command line will override the value in the YAML file and Erigon will run on the Holesky testnet.

## TOML

```bash
./build/bin/erigon --config ./config.toml
```

Example of setting up TOML config file:

```toml
datadir = 'your datadir'
chain = "mainnet"
http = true
"http.api" = ["eth","debug","net"]
```

