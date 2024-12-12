# Tips for faster syncing


## Optimize for Low Latency

Use a machine with low-latency storage (focused on latency, not throughput) and ample RAM to speed up the initial sync process.

## Memory Optimized Nodes

Consider using memory-optimized nodes for faster sync, such as *AWS EC2 r5* or *r6* series instances, for faster syncing.

## Additional Recommendations

- Only expose ports that are necessary for specific use cases (e.g., JSON-RPC or WebSocket).
- Regularly review and audit your firewall rules to ensure they align with your infrastructure needs.
- Utilize monitoring tools like Prometheus or Grafana to track P2P communication metrics.

This minimal configuration ensures proper P2P functionality for both the Execution and Consensus layers, without exposing unnecessary services.