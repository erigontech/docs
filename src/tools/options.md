# Options

The following flags can be used to configure various parameters of the Diagnostics Tool.

## Configuration File:

- `--config` : Specify a configuration file (default is `$HOME/.cobra.yaml`).

## Network Settings:

- `--addr` : Network interface to listen on (default is `localhost`).
- `--port` : Port to listen on (default is `8080`).

## Session Management:

- `--node.sessions` : Maximum number of node sessions to allow (default is `5000`).
- `--ui.sessions` : Maximum number of UI sessions to allow (default is `5000`).

## Logging Configuration:

- `--log.dir.path` : Directory path to store log data (default is `./logs`).
- `--log.file.name` : Name of the log file (default is `diagnostics.log`).
- `--log.file.size.max` : Maximum size of log file in megabytes (default is `100`).
- `--log.file.age.max` : Maximum age in days a log file can persist in the system (default is `28`).
- `--log.max.backup` : Maximum number of log files that can persist (default is `5`).
- `--log.compress` : Whether to compress historical log files (default is `false`).


# Other options

To display other available options for Diagnostics Tool digit:

```bash
cd erigon
./build/bin/erigon support --help
```

The `--help` flag listing is reproduced below for your convenience.

- `--diagnostics.addr [value]`: By default, the diagnostics address is `localhost:8080`. You may tunnel it to connect to a remote node, you must specify it for this flag.
- `--debug.addrs [value]`: Comma separated list of URLs to the debug endpoints thats are being diagnosed [`15sk` ] (default: "localhost:6062")
- `--diagnostics.addr [value]`: Address of the diagnostics system provided by the support team, include unique session PIN (default: "`localhost:8080`")
- `--diagnostics.sessions [value]`: Comma separated list of session PINs to connect to
- `--pprof`: Enable the pprof HTTP server (default: false)
- `--pprof.addr [value]`: pprof HTTP server listening interface (default: "`127.0.0.1`")
- `--pprof.port [value]`: pprof HTTP server listening port (default: `6060`)
- `--pprof.cpuprofile [value]`: Write CPU profile to the given file
- `--trace [value]`: Write execution trace to the given file
- `--help`, `-h`: show help