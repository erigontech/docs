# Software Requirements

Before we start, please note that building software from source can be complex. If you're not comfortable with technical tasks, you might want to check the [Docker](./docker.md) installation.

Erigon works only from command line interface (CLI), so it is advisable to have a good confidence with basic commands.

Please ensure that the following prerequisites are met.

### Build essential (only for Linux)

Install **Build-essential** and **Cmake**:

```bash
sudo apt install build-essential cmake -y
```

### Git

Git is a tool that helps download and manage the Erigon source code. To install Git, visit:

[https://git-scm.com/downloads](https://git-scm.com/downloads).


### Go Programming Language

Erigon utilizes Go (also known as Golang) version 1.22 or newer for part of its development. It is recommended to have a fresh Go installation. If you have an older version, consider deleting the /usr/local/go folder (you may need to use sudo) and re-extract the new version in its place.

To install the latest Go version, visit the official documentation at [https://golang.org/doc/install](https://golang.org/doc/install).

For Linux users, use the following command in your terminal:

```bash
sudo apt-get update                                            
wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
sudo tar -xvf go1.21.0.linux-amd64.tar.gz
sudo mv go /usr/local
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
source ~/.profile
```

### C++ Compiler

This turns the C++ part of Erigon's code into a program your computer can run. You can use either **Clang** or **GCC**.

- For **Clang** follow the instructions at [https://clang.llvm.org/get_started.html](https://clang.llvm.org/get_started.html). Only in Linux, place your terminal to directory where you want to install Clang and copy-paste this code:

```bash
git clone --depth=1 https://github.com/llvm/llvm-project.git
    cd llvm-project
    mkdir build
    cd build
    cmake -DLLVM_ENABLE_PROJECTS=clang -DCMAKE_BUILD_TYPE=Release -G "Unix Makefiles" ../llvm
```

- For **GCC** (version 10 or newer): [https://gcc.gnu.org/install/index.html](https://gcc.gnu.org/install/index.html)

You can now proceed with Erigon installation.