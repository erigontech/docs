# Usage

# All-in-One Client

<div class="warning">
Hint: Before running Erigon you should decide which type of node you want to run.
</div>

The all-in-one client is the preferred option for most users. The following CLI command allows you to run an Ethereum archive node where every process is integrated and no special configuration is needed (all-in-one client):

./build/bin/erigon

# Testnets

If you would like to give Erigon a try, but do not have spare 2TB on your drive, a good option is to start syncing one of the public testnets, Holesky, adding the option `--chain=holesky` and using the default Consensus Layer, Caplin. You can also had the flag `--prune.mode=minimal` to have a node that is syncing fast while taking not so much disk space:

```bash
./build/bin/erigon --chain=holesky --prune.mode=minimal
```

# Help

Running `make help` will list and describe the convenience commands available in the Makefile.

```
go-version:                        print and verify go version
validate_docker_build_args:        ensure docker build args are valid
docker:                            validate, update submodules and build with docker
setup_xdg_data_home:               TODO
docker-compose:                    validate build args, setup xdg data home, and run docker-compose up
dbg                                debug build allows see C stack traces, run it with GOTRACEBACK=crash. You don't need debug build for C pit for profiling. To profile C code use SETCGOTRCKEBACK=1
geth:                              run erigon (TODO: remove?)
erigon:                            build erigon
all:                               run erigon with all commands
db-tools:                          build db tools
test:                              run unit tests with a 100s timeout
test-integration:                  run integration tests with a 30m timeout
lint:                              run golangci-lint with .golangci.yml config file
lintci:                            run golangci-lint (additionally outputs message before run)
lintci-deps:                       (re)installs golangci-lint to build/bin/golangci-lint
clean:                             cleans the go cache, build dir, libmdbx db dir
devtools:                          installs dev tools (and checks for npm installation etc.)
bindings:                          generate test contracts and core contracts
prometheus:                        run prometheus and grafana with docker-compose
escape:                            run escape path={path} to check for memory leaks e.g. run escape path=cmd/erigon
git-submodules:                    update git submodules
user_linux:                        create "erigon" user (Linux)
user_macos:                        create "erigon" user (MacOS)
coverage:                          run code coverage report and output total coverage %
hive:                              run hive test suite locally using docker e.g. OUTPUT_DIR=~/results/hive SIM=ethereum/engine make hive
automated-tests                    run automated tests (BUILD_ERIGON=0 to prevent erigon build with local image tag)
help:                              print commands help
```

