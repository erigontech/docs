# Browser Interface

By navigating to <http://localhost:8080> in your browser, you can access the Diagnostics Tool and explore its various sections. These sections provide a comprehensive overview of your Erigon node's status and activity, covering aspects such as session details, node configuration, network interactions, download status, log files, and more.

1. **Status Bar**: Displays essential information about the current session and operating Erigon node.
2. **Process Tab**:
	* **Command**: Inspect the command line arguments used to launch the Erigon node.
	* **Flags**: Examine the flags set in the CLI context by the user when launching the node.
	* **Node info**: Contains detailed information about the Erigon node.
3. **Network Tab**:
	* **Peers Data**: Collect and view information about network peers, including active peers, static peers, and total seen peers.
	* **Downloader**: Provides detailed information about the progress, download status, estimated time, and resource allocation for "Snapshots" download.
4. **Logs Tab**: View and download logs from the Erigon node, with log rotation and filtering capabilities.
5. **Data Tab**: Inspect databases and their tables.
6. **Admin Tab**:
	* **Session Management**: View active sessions, create new sessions, and obtain session PINs for connections.
	* **Data Management**: Clear all sessions and data .
7. **Available Flags**: Configure various parameters of the diagnostics UI, including network settings, session management, logging configuration, and more.

See currently implemented diagnostics [here](https://github.com/erigontech/diagnostics/blob/main/README.md#currently-implemented-diagnostics).