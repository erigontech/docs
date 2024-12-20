# Downloader
*Seeding/downloading historical data*

The Downloader is a service responsible for seeding and downloading historical data using the BitTorrent protocol. Data is stored in the form of immutable `.seg` files, known as **snapshots**. The Ethereum core instructs the Downloader to download specific files, identified by their unique info hashes, which include both block headers and block bodies. The Downloader then communicates with the BitTorrent network to retrieve the necessary files, as specified by the Ethereum core.

<div class="warning">

**Information**:

While all Erigon components are separable and can be run on different machines, the downloader must run on the same machine as Erigon to be able to share downloaded and seeded files.

</div>

Like many other Erigon components (txpool, sentry, rpc daemon) `downloader` can be running [integrated into Erigon](#start-erigon-with-snapshots-support) or as a [separate process](#running-downloader-as-a-separate-process).

## Start Erigon with snapshots support


Downloader is running by default inside Erigon, where it can be configured with the `--snapshots` flag:

```bash
./build/bin/erigon  --snapshots 
```

The `--snapshots` flag is compatible with the `--prune.mode` flag.

When you start the Erigon node with the --snapshots flag, it allows you to control the behavior of the Downloader component, such as:

- Enabling or disabling the Downloader component
- Configuring the Downloader to use specific snapshots or directories
- Controlling the seeding and downloading of snapshots

## Running downloader as a separate process

Before using a separate downloader process the executable must be built:

```bash
cd erigon
make downloader
```
Downloader can then be started as independent process, for example:

```bash
./build/bin/downloader --downloader.api.addr=127.0.0.1:9093 --torrent.port=42068
```

- `--downloader.api.addr` is for internal communication with Erigon;
- `--torrent.port=42068` is for public BitTorrent protocol listen;
- The default download speed is 16mb/sec. You can increase/limit the network usage by adding the flags `--torrent.download.rate=512mb --torrent.upload.rate=512mb` 
- On startup Erigon sends list of `.torrent` files to Downloader and waits for 100% download completion
    ```bash
    ./build/bin/erigon --snapshots --downloader.api.addr=127.0.0.1:9093
    ```
- Use `--snap.keepblocks=true` to not delete retired blocks from DB.
- Any network/chain can start with snapshot sync:
    - The node will only download snapshots that are registered in the next repository, which can be found at <https://github.com/erigontech/erigon-snapshot>.
    - The node will periodically clear out old blocks from the database by copying them into snapshots of 1,000-block size. It will then merge these snapshots into larger ranges until it reaches snapshots of 500,000 blocks. Once this process is complete, the node will automatically begin creating new snapshots.".

## Creation of a new network or bootnode

When creating a new network or bootnode, it's possible that new snapshots may need to be created and seeded. To do this, you'll need to create the snapshots using the following command:

```bash
erigon snapshots retire --datadir=<your_datadir>
```

This will create .torrent files that the Downloader can use to seed the new snapshots. The output format is compatible with <https://github.com/ledgerwatch/erigon-snapshot>.

To change the size of the snapshots, add the following flags:

```bash
--from=0 --to=1_000_000 --segment.size=500_000
```

Then, use the downloader command to rebuild the snapshots:

```bash
./build/bin/downloader torrent_hashes --rebuild --datadir=<your_datadir>
```

The Downloader will automatically seed the new snapshots.

Note that while Erigon is not required to seed snapshots, running Erigon with the --snapshots flag will also enable seeding.

## Additional info

When creating snapshots, you don't need a fully-synced Erigon node. In fact, you only need to complete a few initial stages of syncing. This allows you to start seeding snapshots without having to wait for a full sync.

To take advantage of this, you can use the following flags to start syncing, but only seed the first few stages:

- `STOP AFTER STAGE=Senders`: this flag tells Erigon to stop syncing after reaching the "Senders" stage. This allows you to seed the snapshots without waiting for the full sync.
- `./build/bin/erigon --snapshots=false --datadir=<your_datadir>`: this command starts the Erigon node in snapshot-only mode, which allows it to seed the snapshots without waiting for the full sync.

However, for security reasons, it's highly recommended to have a fully-synced Erigon node. This ensures that all data is up-to-date and secure.

### Indexing Snapshots Before Seeding

Before seeding snapshots, they must be indexed by Erigon. While indexing is not required for seeding, it's recommended to run the following command to ensure that snapshots are properly indexed:

```bash
./build/bin/erigon snapshots index --datadir=<your_datadir>
```

This step is not required for seeding, but it's essential for using snapshots effectively.

## Architecture

Snapshots can be created in four ways:

1. **Automated creation**: Erigon can create new .torrent files using the downloader.Download RPC method.
2. **Manual creation**: Erigon can create new .seg files, which are then scanned by the Downloader to create .torrent files.
3. **Manual seeding**: .torrent files can be manually copied from another server or restored from backup.
4. **Manual indexing**: .seg files can be manually copied and indexed by the Downloader.

**Erigon**'s role in the snapshot creation process:
- Connects to the Downloader and shares the list of hashes.
- Waits for the download of all snapshots.
- Creates `.idx` files (secondary indices) when .seg files are available.
- Switches to normal staged sync after downloading all snapshots.
- Ensures that snapshot downloading happens only once, even if new Erigon versions are released.

**Downloader**'s role in the snapshot creation process:
- Reads .torrent files and downloads the contents described by them.
- Uses a list of trackers to download files (see ./trackers/embed.go).
- Automatically seeds the downloaded files.

# Technical Details

To prevent attacks, `.idx` files are created with random seeds, ensuring that each node has a unique `.idx` file (but the same `.seg` file).
If `.seg` files are manually added or removed, the `<your_datadir>/snapshots/db` folder must also be updated.

## Verifying .seg file checksums

Use the `downloader --verify` command to check the checksums of the `.seg` files. Compare the checksums with those of the current `.torrent` files.

## Faster Rsync

Use the following command to perform a faster rsync:
```bash
rsync -aP --delete -e "ssh -T -o Compression=no -x"
```

## Release Details

To start automatic commits of new hashes to the master branch:
```bash
crontab -e @hourly cd <erigon_source_dir> && ./cmd/downloader/torrent_hashes_update.sh <your_datadir> <network_name> 1>&2 2>> ~/erigon_cron.log
```

This command pushes the changes to the master branch automatically before each release.

# Command line options

To display available options for downloader digit:

```bash
./build/bin/downloader --help
```

The `--help` flag listing is reproduced below for your convenience.

```bash
snapshot downloader

Usage:
   [flags]
   [command]

Examples:
go run ./cmd/downloader --datadir <your_datadir> --downloader.api.addr 127.0.0.1:9093

Available Commands:
  completion      Generate the autocompletion script for the specified shell
  help            Help about any command
  manifest        
  manifest-verify 
  torrent_cat     
  torrent_clean   Remove all .torrent files from datadir directory
  torrent_create  
  torrent_hashes  
  torrent_magnet  

Flags:
      --chain string                       name of the network to join (default "mainnet")
      --datadir string                     Data directory for the databases (default "/home/usr/.local/share/erigon")
      --db.writemap                        Enable WRITE_MAP feature for fast database writes and fast commit times (default true)
      --diagnostics.disabled               Disable diagnostics
      --diagnostics.endpoint.addr string   Diagnostics HTTP server listening interface (default "127.0.0.1")
      --diagnostics.endpoint.port uint     Diagnostics HTTP server listening port (default 6062)
      --diagnostics.speedtest              Enable speed test
      --downloader.api.addr string         external downloader api network address, for example: 127.0.0.1:9093 serves remote downloader interface (default "127.0.0.1:9093")
      --downloader.disable.ipv4            Turns off ipv6 for the downloader
      --downloader.disable.ipv6            Turns off ipv6 for the downloader
  -h, --help                               help for this command
      --log.console.json                   Format console logs with JSON
      --log.console.verbosity string       Set the log level for console logs (default "info")
      --log.delays                         Enable block delay logging
      --log.dir.disable                    disable disk logging
      --log.dir.json                       Format file logs with JSON
      --log.dir.path string                Path to store user and error logs to disk
      --log.dir.prefix string              The file name prefix for logs stored to disk
      --log.dir.verbosity string           Set the log verbosity for logs stored to disk (default "info")
      --log.json                           Format console logs with JSON
      --metrics                            Enable metrics collection and reporting
      --metrics.addr string                Enable stand-alone metrics HTTP server listening interface (default "127.0.0.1")
      --metrics.port int                   Metrics HTTP server listening port (default 6061)
      --nat string                         NAT port mapping mechanism (any|none|upnp|pmp|stun|extip:<IP>)
                                           			 "" or "none"         Default - do not nat
                                           			 "extip:77.12.33.4"   Will assume the local machine is reachable on the given IP
                                           			 "any"                Uses the first auto-detected mechanism
                                           			 "upnp"               Uses the Universal Plug and Play protocol
                                           			 "pmp"                Uses NAT-PMP with an auto-detected gateway address
                                           			 "pmp:192.168.0.1"    Uses NAT-PMP with the given gateway address
                                           			 "stun"               Uses STUN to detect an external IP using a default server
                                           			 "stun:<server>"      Uses STUN to detect an external IP using the given server (host:port)
                                           
      --pprof                              Enable the pprof HTTP server
      --pprof.addr string                  pprof HTTP server listening interface (default "127.0.0.1")
      --pprof.cpuprofile string            Write CPU profile to the given file
      --pprof.port int                     pprof HTTP server listening port (default 6060)
      --seedbox                            Turns downloader into independent (doesn't need Erigon) software which discover/download/seed new files - useful for Erigon network, and can work on very cheap hardware. It will: 1) download .torrent from webseed 2) download new files after upgrade 3) we planing add discovery of new files soon
      --torrent.conns.perfile int          Number of connections per file (default 10)
      --torrent.download.rate string       Bytes per second, example: 32mb (default "128mb")
      --torrent.download.slots int         Amount of files to download in parallel. (default 128)
      --torrent.maxpeers int               Unused parameter (reserved for future use) (default 100)
      --torrent.port int                   Port to listen and serve BitTorrent protocol (default 42069)
      --torrent.staticpeers string         Comma separated host:port to connect to
      --torrent.upload.rate string         Bytes per second, example: 32mb (default "4mb")
      --torrent.verbosity int              0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (must set --verbosity to equal or higher level and has default: 2) (default 2)
      --trace string                       Write execution trace to the given file
      --verbosity string                   Set the log level for console logs (default "info")
      --verify                             Verify snapshots on startup. It will not report problems found, but re-download broken pieces.
      --verify.failfast                    Stop on first found error. Report it and exit
      --verify.files string                Limit list of files to verify
      --webseed string                     Comma-separated URL's, holding metadata about network-support infrastructure (like S3 buckets with snapshots, bootnodes, etc...)

Use " [command] --help" for more information about a command.
```