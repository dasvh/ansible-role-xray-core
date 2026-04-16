# Ansible Role: Xray-core Setup

Installs and configures [Xray-core](https://github.com/XTLS/Xray-core), a platform for building proxies to bypass network restrictions. It specifically focuses on setting up **REALITY**, a next-generation security protocol that eliminates TLS fingerprinting by mimicking the behavior of a real, popular website (like `microsoft.com`).

## Features

- Installs Xray-core from official GitHub releases
- Configures REALITY with automated key generation
- Supports multiple transport protocols (TCP/VISION, gRPC, xhttp)
- Generates per-client share links ready for use in clients (see [Xray-core](https://github.com/XTLS/Xray-core/blob/main/README.md#gui-clients))

## Requirements

- Ansible 2.9 or higher.
- Target system: **Ubuntu 24.04 (Noble)** (Tested and verified)

## Role Variables

The following variables can be overridden to customize the installation.

| Variable                   | Default Value            | Description                                         |
| -------------------------- | ------------------------ | --------------------------------------------------- |
| `xray_version`             | `v26.3.28`               | The version of Xray-core to install.                |
| `xray_install_dir`         | `/opt/xray`              | Directory to install Xray binaries.                 |
| `xray_config_dir`          | `/etc/xray`              | Directory for Xray configuration files.             |
| `xray_bin_path`            | `/usr/local/bin/xray`    | Full path to the Xray binary.                       |
| `xray_client_output_dir`   | `/root/xray-clients`     | Directory to save generated client share links.     |
| `xray_port`                | `443`                    | The main inbound port for Xray (TCP/VISION).        |
| `xray_grpc_port`           | `8443`                   | The inbound port for gRPC.                          |
| `xray_xhttp_port`          | `9443`                   | The inbound port for xhttp.                         |
| `xray_protocol`            | `tcp`                    | The transport protocol to use.                      |
| `xray_reality_fingerprint` | `chrome`                 | The uTLS fingerprint for REALITY.                   |
| `xray_reality_target`      | `www.microsoft.com`      | The destination for REALITY handshaking.            |
| `xray_reality_server_name` | `www.microsoft.com`      | The server name to match for REALITY.               |
| `xray_clients`             | `[]`                     | A list of client objects. **This must be set.**     |

### Example `xray_clients` format:

```yaml
xray_clients:
  - name: my-phone
    id: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  - name: my-laptop
    id: "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"
```

## Maintenance

### Updating Xray
To update Xray to a newer version, update the `xray_version` variable in your inventory and rerun the playbook. The role will automatically download, unpack, and install the new binary.

## License

MIT
