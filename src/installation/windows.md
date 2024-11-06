# Windows
*How to install and run Erigon 3 on Windows*

There are 3 options for running Erigon 3 on Windows, listed from easiest to most difficult installation:

-   [Build executable binaries natively for Windows](#build-executable-binaries-natively-for-windows): Use the pre-built Windows executables that can be natively run on Windows without any emulation or containers required.
    
-   [Use Docker](/installation/docker.md): Run Erigon in a Docker container for isolation from the host Windows system. This avoids dependencies on Windows but requires installing Docker.
    
-   [Use Windows Subsystem for Linux (WSL)](#use-windows-subsystem-for-linux-wsl): Install the Windows Subsystem for Linux (WSL) to create a Linux environment within Windows. Erigon can then be installed in WSL by following the Linux build instructions. This provides compatibility with Linux builds but involves more setup overhead.
    

## Build executable binaries natively for Windows

Before proceeding, ensure that the [hardware](/getting-started/hw-requirements.md) and [software](/getting-started/sw-requirements.md) requirements are met.

### Installing Chocolatey

Install _Chocolatey package manager_ by following these [instructions](https://docs.chocolatey.org/en-us/choco/setup).

Once your Windows machine has the above installed, open the **Command Prompt** by typing "**cmd**" in the search bar and check that you have correctly installed Chocolatey:

```bash
choco -v
```

<img src="/images/choco-v.png" alt="" style="display: block; margin: 0 auto;">

Now you need to install the following components: `cmake`, `make`, `mingw` by:

```bash
choco install cmake make mingw
```

<div class="warning">

**Important note about Anti-Virus:**

During the compiler detection phase of **MinGW**, some temporary executable files are generated to test the compiler capabilities. It's been reported that some anti-virus programs detect these files as possibly infected with the `Win64/Kryptic.CIS` Trojan horse (or a variant of it). Although these are false positives, we have no control over the 100+ vendors of security products for Windows and their respective detection algorithms and we understand that this may make your experience with Windows builds uncomfortable. To work around this, you can either set exclusions for your antivirus software specifically for the`build\bin\mdbx\CMakeFiles` subfolder of the cloned repo, or you can run Erigon using the other two options below.

</div>

Make sure that the Windows System Path variable is set correctly. Use the search bar on your computer to search for “**Edit the system environment variable**”.

<img src="/images/Edit_sys_env.png" alt="" style="display: block; margin: 0 auto;">

Click the “**Environment Variables...**” button.

<img src="/images/Edit_sys_env2.png" alt="" style="display: block; margin: 0 auto;">

Look down at the "**System variables**" box and double click on "**Path**" to add a new path.

<img src="/images/System_var.png" alt="" style="display: block; margin: 0 auto;">

Then click on the "**New**" button and paste the following path:

```bash
 C:\ProgramData\chocolatey\lib\mingw\tools\install\mingw64\bin
```

<img src="/images/new_sys_var.png" alt="" style="display: block; margin: 0 auto;">


### Clone the Erigon repository

Open the Command Prompt and type the following:

```bash
git clone --branch v3.0.0-alpha5 --single-branch https://github.com/erigontech/erigon.git
```

### Compiling Erigon

To compile Erigon there are two alternative methods:

-   [Compiling from the wmake.ps1 file in the File Explorer](#compiling-from-the-wmakeps1-file-in-the-file-explorer)
    
-   [Using the PowerShell CLI](#using-the-powershell-cli)
    

#### Compiling from the wmake.ps1 file in the File Explorer

This is the fastest way which normally works for everyone. Open the File Explorer and go to the Erigon folder, then right click the `wmake` file and choose "**Run with PowerShell**".

<img src="/images/powershell.png" alt="" style="display: block; margin: 0 auto;">

PowerShell will compile Erigon and all of its modules. All binaries will be placed in the `.\build\bin\` subfolder.

<img src="/images/powershell2.png" alt="" style="display: block; margin: 0 auto;">

#### Using the PowerShell CLI

In the search bar on your computer, search for “**Windows PowerShell**” and open it.

<img src="/images/powershell3.png" alt="" style="display: block; margin: 0 auto;">

Change the working directory to "**erigon**"

```bash
cd erigon
```

<img src="/images/powershell4.png" alt="" style="display: block; margin: 0 auto;">

Before proceeding make sure that the [Set-Execution Policy]
(https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.3) - PowerShell execution running policies are correct for your Windows account.

Now you can compile Erigon and/or any of its component:

```bash
.\wmake.ps1 [-target] <targetname>
```

For example, to build the Erigon executable write:

```
.\wmake.ps1 erigon
```

<img src="/images/powershell5.png" alt="" style="display: block; margin: 0 auto;">

You can use the same command to build other binaries as RPCDaemon, TxPool, Sentry and Downloader.

All binaries are placed in the `.\build\bin\` subfolder.

## Use Windows Subsystem for Linux (WSL)

WSL enables running a complete GNU/Linux environment natively within Windows 10, providing Linux compatibility without the performance overhead of traditional virtualization.

To install WSL, follow these instructions: <https://learn.microsoft.com/en-us/windows/wsl/install>.

<div class="warning">

**Information**

WSL Version 2 is the only version supported.

</div>

Under this option you can build Erigon as you would on a regular Linux distribution (see detailed instructions [here](/installation/linux.md)).

You can also point your data to any of the mounted Windows partitions ( e.g. `/mnt/c/[...]`, `/mnt/d/[...]` etc..) but be aware that performance will be affected: this is due to the fact that these mount points use `DrvFS`, which is a network file system, and additionally MDBX locks the db for exclusive access, meaning that only one process at a time can access the data.

<div class="warning">

**Warning**

The remote db RPCdaemon is an experimental feature and is **not recommended**, it is extremely slow. It is highly preferable to use the embedded RPCdaemon.

</div>


This has implications for running `rpcdaemon`, which must be configured as a remote DB, even if it is running on the same machine. If your data is hosted on the native Linux filesystem instead, there are no restrictions. Also note that the default WSL2 environment has its own IP address, which does not match the network interface of the Windows host: take this into account when configuring NAT on port 30303 on your router.
