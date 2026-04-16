# Ansible Role: Xray-core Setup

This Ansible role installs and configures xray-core with a focus on a REALITY setup.

## Requirements

Ansible 2.9 or higher.

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

This variable must be defined in your `group_vars` or `host_vars`.

```yaml
xray_clients:
  - name: my-phone
    id: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  - name: my-laptop
    id: "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"
```

## License

MIT
