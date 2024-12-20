# Default Ports and Firewalls

Main recommendations:

- Avoid exposing other ports unless necessary for specific use cases (e.g., JSON-RPC or WebSocket).
- Regularly audit your firewall rules to ensure they are aligned with your infrastructure needs.
- Use monitoring tools like Prometheus or Grafana to track P2P communication metrics.

This minimal configuration ensures proper P2P functionality for both the Execution and Consensus layers without exposing unnecessary services. Let me know if you need further clarifications!

Too see ports used by Erigon and its components refer to <https://github.com/erigontech/erigon?tab=readme-ov-file#default-ports-and-firewalls>.