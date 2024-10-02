# Windows
*How to install and run Erigon 3 on Windows*

There are 3 options for running Erigon 3 on Windows, listed from easiest to most difficult installation:

-   [Build executable binaries natively for Windows](https://erigon.gitbook.io/erigon/basic-usage/getting-started/windows#build-executable-binaries-natively-for-windows): Use the pre-built Windows executables that can be natively run on Windows without any emulation or containers required.
    
-   [Use Docker](https://erigon.gitbook.io/erigon/basic-usage/getting-started/windows#use-docker): Run Erigon in a Docker container for isolation from the host Windows system. This avoids dependencies on Windows but requires installing Docker.
    
-   [Use Windows Subsystem for Linux (WSL)](https://erigon.gitbook.io/erigon/basic-usage/getting-started/windows#use-windows-subsystem-for-linux-wsl): Install the Windows Subsystem for Linux (WSL) to create a Linux environment within Windows. Erigon can then be installed in WSL by following the Linux build instructions. This provides compatibility with Linux builds but involves more setup overhead.
    

## Build executable binaries natively for Windows

Before proceeding, ensure that the general [requirements](https://erigon.gitbook.io/erigon/basic-usage/getting-started#hardware-requirements) are met.

### Installing Chocolatey

Install _Chocolatey package manager_ by following these [instructions](https://docs.chocolatey.org/en-us/choco/setup).

Once your Windows machine has the above installed, open the **Command Prompt** by typing "**cmd**" in the search bar and check that you have correctly installed Chocolatey:

```bash
choco -v
```

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FAqRNiSe3JRMH48RnpU4M%252Fimage.png%3Falt%3Dmedia%26token%3Dd4bf4d87-59cd-4e49-b1d2-73b0f7343e79&width=768&dpr=4&quality=100&sign=1819d0c1&sv=1)

Now you need to install the following components: `cmake`, `make`, `mingw` by:

```bash
choco install cmake make mingw
```

**Important note about Anti-Virus:** During the compiler detection phase of MinGW, some temporary executable files are generated to test the compiler capabilities. It's been reported that some anti-virus programs detect these files as possibly infected with the `Win64/Kryptic.CIS` Trojan horse (or a variant of it). Although these are false positives, we have no control over the 100+ vendors of security products for Windows and their respective detection algorithms and we understand that this may make your experience with Windows builds uncomfortable. To work around this, you can either set exclusions for your antivirus software specifically for the`build\bin\mdbx\CMakeFiles` subfolder of the cloned repo, or you can run Erigon using the other two options below.

Make sure that the Windows System Path variable is set correctly. Use the search bar on your computer to search for “**Edit the system environment variable**”.

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FuIzFzKRHIJea46qAGYyK%252Fimage.png%3Falt%3Dmedia%26token%3D6941fac4-f496-4c99-a8f2-06e28a276132&width=768&dpr=4&quality=100&sign=6724aff&sv=1)

Click the “**Environment Variables...**” button.

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FFJQDBBaCqwxlu74Rj7Gk%252Fimage.png%3Falt%3Dmedia%26token%3D721c97df-5f99-4057-88de-6d86f1ccc827&width=768&dpr=4&quality=100&sign=358f342b&sv=1)

Look down at the "**System variables**" box and double click on "**Path**" to add a new path.

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252F8J83HtpBXEbK8JlCaQ57%252Fimage.png%3Falt%3Dmedia%26token%3Dd1914858-11e6-43cd-bd78-51825a4c8e62&width=768&dpr=4&quality=100&sign=a87846e9&sv=1)

Then click on the "**New**" button and paste the path here:

```bash
 C:\ProgramData\chocolatey\lib\mingw\tools\install\mingw64\bin
```

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FcxwhuppIN2sOfYg3HUcT%252Fpath2.png%3Falt%3Dmedia%26token%3D090c5597-2359-4bba-8f0b-009d8c82a92d&width=768&dpr=4&quality=100&sign=91f964&sv=1)

### Clone the Erigon repository

Make sure you have Git installed, see [https://git-scm.com/downloads](https://git-scm.com/downloads).

Open the Command Prompt and type the following:

```bash
git clone --branch 3.0.0 --single-branch https://github.com/ledgerwatch/erigon.git
```

### Compiling Erigon

To compile Erigon there are two alternative methods:

-   [Compiling from the wmake.ps1 file in the File Explorer](https://erigon.gitbook.io/erigon/basic-usage/getting-started/windows#compiling-from-the-wmake.ps1-file-in-the-file-explorer)
    
-   [Using the PowerShell CLI](https://erigon.gitbook.io/erigon/basic-usage/getting-started/windows#using-the-powershell-cli)
    

#### Compiling from the wmake.ps1 file in the File Explorer

This is the fastest way which normally works for everyone. Open the File Explorer and go to the Erigon folder, then right click the `wmake` file and choose "**Run with PowerShell**".

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FfcOUUMOW0CBtqd7WxEHM%252FImmagine%25202023-09-25%2520162444.png%3Falt%3Dmedia%26token%3D7875e451-f979-424f-9e64-a4ab4ffa0afc&width=768&dpr=4&quality=100&sign=c7b8d74e&sv=1)

PowerShell will compile Erigon and all of its modules. All binaries are placed in the `.\build\bin\` subfolder.

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FK58q89hk9IXqScpJzhkG%252Fimage.png%3Falt%3Dmedia%26token%3D29a9e074-789a-4000-b581-094e212e4660&width=768&dpr=4&quality=100&sign=165ad893&sv=1)

#### Using the PowerShell CLI

In the search bar on your computer, search for “**Windows PowerShell**” and open it.

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252FEmMVQg8OI9d0Wm0wxzrG%252Fimage.png%3Falt%3Dmedia%26token%3D822abe0e-3ecb-4e29-8a98-ae4306cf37f8&width=768&dpr=4&quality=100&sign=20a0e02f&sv=1)

Change the working directory to "**erigon**"

```bash
cd erigon
```

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252F3lMY5KBR6nnYpOOL0XtN%252Fimage.png%3Falt%3Dmedia%26token%3D51c370f0-1582-4062-b84e-7deecfce5319&width=768&dpr=4&quality=100&sign=38e16017&sv=1)

Before proceeding make sure that the [Set-Execution Policy](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.3) PowerShell execution running policies are correct for your Windows account.

Now you can compile Erigon and/or any of its component:

```bash
.\wmake.ps1 [-target] <targetname>
```

For example, to build the Erigon executable write:

```
.\wmake.ps1 erigon
```

![](https://erigon.gitbook.io/~gitbook/image?url=https%3A%2F%2F2414554083-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Feeqc6D5KqkgOsOW7j4k6%252Fuploads%252Fwaw42ktWXUvjGGlpXMES%252Fimage.png%3Falt%3Dmedia%26token%3Dc09b3df7-521a-4dd6-ac69-f5592f544cb8&width=768&dpr=4&quality=100&sign=21fcbbb5&sv=1)

You can also build other binaries as [RPCDaemon](https://erigon.gitbook.io/erigon/advanced-usage/rpc-daemon), [TxPool](https://erigon.gitbook.io/erigon/advanced-usage/txpool), [Sentry](https://erigon.gitbook.io/erigon/advanced-usage/sentry) and [Downloader](https://erigon.gitbook.io/erigon/advanced-usage/downloader).

All binaries are placed in the `.\build\bin\` subfolder.

## Use Docker

See [docker instructions](https://erigon.gitbook.io/erigon/basic-usage/getting-started/docker).

## Use Windows Subsystem for Linux (WSL)

WSL enables running a complete GNU/Linux environment natively within Windows 10, providing Linux compatibility without the performance overhead of traditional virtualization.

To install WSL, follow these instructions: [https://learn.microsoft.com/en-us/windows/wsl/install](https://learn.microsoft.com/en-us/windows/wsl/install).

**Information:** WSL Version 2 is the only version supported.

Under this option you can build Erigon as you would on a regular Linux distribution (see detailed instructions [here](https://erigon.gitbook.io/erigon/basic-usage/getting-started/linux-and-macos)).

You can also point your data to any of the mounted Windows partitions ( e.g. `/mnt/c/[...]`, `/mnt/d/[...]` etc..) but be aware that performance will be affected: this is due to the fact that these mount points use `DrvFS`, which is a network file system, and additionally MDBX locks the db for exclusive access, meaning that only one process at a time can access the data.

**Warning**: the remote db RPCdaemon is an experimental feature and is **not recommended**, it is extremely slow. It is highly preferable to use the embedded RPCdaemon.

This has implications for running `rpcdaemon`, which must be configured as a remote DB, even if it is running on the same machine. If your data is hosted on the native Linux filesystem instead, there are no restrictions. Also note that the default WSL2 environment has its own IP address, which does not match the network interface of the Windows host: take this into account when configuring NAT on port 30303 on your router.
