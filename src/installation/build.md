# Build Erigon from source
*How to build Erigon in Linux and MacOS from source*

The basic Erigon configuration is suitable for most users just wanting to run a node. For building the latest stable release use the following command:

```bash
git clone --branch release/3.0 --single-branch https://github.com/erigontech/erigon.git
cd erigon
make erigon
```

This should create the binary at `./build/bin/erigon`.