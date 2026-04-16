# Ansible Role: Xray-core Setup

Installs and configures [Xray-core](https://github.com/XTLS/Xray-core), a platform for building proxies to bypass
network restrictions. It specifically focuses on setting up **REALITY**, a next-generation security protocol that
eliminates TLS fingerprinting by mimicking the behavior of a real, popular website (like `microsoft.com`).

## Features

- Installs Xray-core from official GitHub releases
- Configures REALITY with automated key generation
- Supports multiple transport protocols (TCP/VISION, gRPC, xhttp)
- Generates per-client share links ready for use in clients (see [Xray-core](https://github.com/XTLS/Xray-core/blob/main/README.md#gui-clients))
- Simple updates for Xray-core by changing the `xray_version` variable

## Requirements

- Ansible 2.9 or higher.
- Target system: **Ubuntu 24.04 (noble numbat)** (tested on a VPS).

## Security Notes

- **User Privileges:** The Xray process runs as the `xray` user. It uses Linux Capabilities (`CAP_NET_BIND_SERVICE`) to
  allow binding to privileged ports like 443 without requiring root access.
- **Key Generation:** REALITY private keys are generated on the fly on the server if they don't exist. They are stored
  in `{{ xray_config_dir }}/reality_keys.txt` with restricted permissions (400).
- **Client IDs:** You **must** provide a unique UUID for each client. You can generate one using the `uuidgen` command

## Role Variables

The following variables can be overridden to customize the installation.

| Variable                 | Default Value              | Description                                     |
|--------------------------|----------------------------|-------------------------------------------------|
| `xray_version`           | `v26.3.28`                 | The version of Xray-core to install.            |
| `xray_install_dir`       | `/opt/xray`                | Directory to install Xray binaries.             |
| `xray_config_dir`        | `/etc/xray`                | Directory for Xray configuration files.         |
| `xray_bin_path`          | `/usr/local/bin/xray`      | Full path to the Xray binary.                   |
| `xray_client_output_dir` | `/root/xray-clients`       | Directory to save generated client share links. |
| `xray_port`              | `443`                      | The main inbound port for Xray (TCP/VISION).    |
| `xray_transports`        | `['tcp', 'grpc', 'xhttp']` | List of transport protocols to enable.          |
| `xray_clients`           | `[]`                       | A list of client objects (name and UUID `id`).  |

### Example `xray_clients` format:

```yaml
xray_clients:
  - name: my-phone
    id: "1fe00393-c83d-43f0-81ec-cb0ee8074641"
```

## License

This project is licensed under the [MIT License](https://github.com/dasvh/ansible-role-xray-core/raw/main/LICENSE).
