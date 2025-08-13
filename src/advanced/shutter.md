# Shutter Network

## What is Shutter Network?

[Shutter Network](https://www.shutter.network) is a privacy-focused protocol that provides encrypted transaction pools using threshold encryption. The main objective is to protect users from malicious MEV (Miner Extractable Value) attacks such as front-running and sandwich attacks by encrypting transactions until they are included in a block.

The key advantages of Shutter Network are:
- **Protection against MEV attacks:** By encrypting transactions, the network prevents malicious actors from exploiting transaction ordering.
- **Threshold encryption:** Transactions are only decrypted when enough key holders (keypers) participate, ensuring security and decentralization.
- **Support on Gnosis Chain:** Shutter encrypted transaction pools are currently available on [Gnosis Chain](https://docs.gnosischain.com/shutterized-gc/), with plans for Ethereum support.

### Why Use Shutter?

- **Access to Extra Transactions:** Shutterized validators can include shielded transactions not available in the public transaction pool, leading to potentially higher block rewards.
- **User Protection:** Help protect users against MEV attacks, improving the fairness of the chain.

## How to Run Erigon as a Shutterized Validator

To participate in the Shutter encrypted transaction pool as a validator using Erigon, follow these steps:

1. **Set Up Your Validator**

   Deposit your stake and register your validator on Gnosis Chain.  
   Reference: [Gnosis Chain Validator Setup](https://docs.gnosischain.com/node/manual/validator/deposit)

2. **Register as a Shutterized Validator**

   Complete validator registration for Shutter using the provided tool:  
   Reference: [Shutter Validator Registration Guide](https://github.com/NethermindEth/shutter-validator-registration)

3. **Verify Registration**

   Use the Erigon CLI command to verify that your registration was successful:
   ```bash
   erigon shutter-validator-reg-check --chain <CHAIN> --el-url <EL_RPC_URL> --validator-info-file <VALIDATOR_INFO_JSON>
   ```
   - `<VALIDATOR_INFO_JSON>` is the file generated during registration.

4. **Run Erigon with Shutter Support**

   Start Erigon as usual, but add the `--shutter` flag to enable Shutterized Validator mode:
   ```bash
   erigon --shutter [other options...]
   ```
   This works with Erigon's internal CL Caplin (enabled by default) or with an external CL client using `--externalcl`.

## Options

Below are relevant CLI options and configuration settings for Shutter functionality in Erigon:

| Option                                        | Description                                                    |
|-----------------------------------------------|----------------------------------------------------------------|
| `--shutter`                                   | Enables Shutterized Validator mode.                            |
| `--externalcl`                                | Use an external Consensus Layer client instead of Caplin.      |
| `shutter-validator-reg-check`                 | Command to verify Shutter validator registration.              |
| `--chain <CHAIN>`                             | Specifies the chain (e.g., Gnosis).                            |
| `--el-url <EL_RPC_URL>`                       | Sets the execution layer RPC endpoint.                         |
| `--validator-info-file <VALIDATOR_INFO_JSON>` | Path to validator info JSON file produced during registration. |

**Shutter Network Default Port:**  
- `23102` (TCP) — Peering port for Shutter.

**Reference Documentation:**
- [Gnosis Chain Validator Setup](https://docs.gnosischain.com/node/manual/validator/deposit)
- [Shutter Validator Registration](https://github.com/NethermindEth/shutter-validator-registration)
- [Shutter Specs](https://github.com/gnosischain/specs/tree/master/shutter)
- [System Overview Dashboard](https://explorer.shutter.network/system-overview)

