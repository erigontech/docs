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

Git is a tool that helps download and manage the Erigon source code. To install Git, visit [https://git-scm.com/downloads](https://git-scm.com/downloads).


### Go Programming Language

Go (also called Golang) version 1.21 or newer is used to write part of Erigon.

It is recommended to have a new Go installation. In case you have a previous version delete the /usr/local/go folder (you will probably need to usesudo), and re-extract the new version in its place.

Visit [https://golang.org/doc/install](https://golang.org/doc/install) for installation instructions.

For Linux copy-paste this into your terminal:

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

- For GCC (version 10 or newer): [https://gcc.gnu.org/install/index.html](https://gcc.gnu.org/install/index.html)

You can now proceed with Erigon installation.