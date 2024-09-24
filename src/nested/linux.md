# Linux and MacOS
*How to install Erigon in Linux and MacOS*

The basic Erigon configuration is suitable for most users just wanting to run a node. For building the latest stable release use the following command:

```bash
git clone --branch 3.0.0-alpha3 --single-branch https://github.com/erigontech/erigon.git
cd erigon
make erigon
```

This should create the binary at `./build/bin/erigon`.