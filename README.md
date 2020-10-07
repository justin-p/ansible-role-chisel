# ansible-chisel

A Ansible role to deploy a [chisel](https://github.com/jpillora/chisel) client and/or server as a systemd service.

## Requirements

None.

## Variables

`defaults/main.yml`

| Variable                         | Default value                                                                                                             | Explanation                                                 |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| chisel_version                   | 1.7.1                                                                                                                     | The release version of chisel linux amd64 to download.      |
| chisel_download_url_linux_amd64  | `https:\\github.com/jpillora/chisel/releases/download/v{{ chisel_version }}/chisel\_{{ chisel_version }}\_linux_amd64.gz` | The download url.                                           |
| chisel_linux_amd64_sha256        | 6e1611b4524f7426cbd8d7351b269a1239ee710e575e9e460fce110c35962de6                                                          | The sha256 checksum of the downloaded file.                 |
| chisel_download_destination      | /tmp/chisel\_{{ chisel_version }}.gz                                                                                      | The download destination.                                   |
| chisel_install_destination       | /usr/local/bin/chisel                                                                                                     | The location to install chisel.                             |
| chisel_service_name              | chisel-client                                                                                                             | The name of the service that should be installed.           |
| chisel_service_destination       | "/lib/systemd/system/{{ chisel_service_name }}.service"                                                                   | The destination where of the service file should be installed. |
| chisel_service_template          | "{{ chisel_service_name }}.service.j2"                                                                                    | This role has 2 build-in templates, [chisel-client](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-client.service.j2) and [chisel-server](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-server.service.j2). |
| chisel_config_name               | chisel-client                                                                                                             | The name of the chisel config.  |
| chisel_config_folder             | /etc/chisel/                                                                                                              | The folder where the chisel config will be installed.      |
| chisel_config_template           | "{{ chisel_config_name }}.conf.j2"                                                                                        | This role has 2 build-in templates, [chisel-client](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-client.conf.j2) and [chisel-server](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-server.conf.j2). |
| chisel_config_destination        | "{{ chisel_config_folder }}{{ chisel_config_name }}.conf"                                                                 | The full path where the chisel config will be installed.   |
| chisel_client_server_url         | `http://127.0.0.1`                                                                                                        | The URL of the chisel server. |
| chisel_client_remotes            | "8080"                                                                                                                    | The remotes that are tunneled through the server. |
| chisel_client_server_fingerprint | aa:bb:cc:dd:ee:ff:gg                                                                                                      | The fingerprint of the server. |
| chisel_client_auth_username      | user                                                                                                                      | The username to authenticate with. |
| chisel_client_auth_password      | pass                                                                                                                      | The password to authenticate with. |
| chisel_client_keepalive          | 25s                                                                                                                       | The keep alive for the client. |
| chisel_client_max_retry_count    | unlimited                                                                                                                 | The max retry count for the client. |
| chisel_client_max_retry_interval | 5                                                                                                                         | The max retry interval for the client. |
| chisel_client_proxy              | http://admin:password@my-server.com:8081                                                                                  | An optional HTTP CONNECT or SOCKS5 proxy which will be used to reach the chisel server. |
| chisel_client_headers            | '--header "Foo : Bar" --header "Hello : World"'                                                                           | Set a custom header in the form "HeaderName: HeaderContent". |
| chisel_client_hostname           | example.com                                                                                                               | Optionally set the 'Host' header.  |
| chisel_client_tls_ca             | /path/to/bundle                                                                                                           | An optional root certificate bundle used to verify the chisel server. |
| chisel_client_tls_key            | /path/to/PEM                                                                                                              | A path to a PEM encoded private key used for client authentication. |
| chisel_client_tls_cert           | /path/to/PEM                                                                                                              | A path to a PEM encoded certificate matching the provided private key.  |
| chisel_server_host               | 0.0.0.0                                                                                                                   | Defines the HTTP listening host – the network interface. |
| chisel_server_port               | 80                                                                                                                        | Defines the HTTP listening port. |
| chisel_server_key                | a_random_string                                                                                                           | An optional string to seed the generation of a ECDSA keypair. |
| chisel_server_auth_file          | /path/to/user.json                                                                                                        | An optional path to a users.json file. |
| chisel_server_auth               | user:pass                                                                                                                 | An optional string representing a single user with full access. |
| chisel_server_keepalive          | 25s                                                                                                                       | The keep alive for the server. |
| chisel_server_backend            | http://127.0.0.1:8081                                                                                                     | Specifies another HTTP server to proxy requests to when chisel receives a normal HTTP request.|
| chisel_server_tls_ca             | /path/to/PEM                                                                                                              | A path to a PEM encoded CA certificate bundle. |
| chisel_server_tls_key            | /path/to/PEM                                                                                                              | Enables TLS and provides optional path to a PEM-encoded TLS private key. |
| chisel_server_tls_cert           | /path/to/PEM                                                                                                              | Enables TLS and provides optional path to a PEM-encoded TLS certificate. |

## Dependencies

None.

## Example Playbooks

### Client with example template

```yml
---
- hosts: local
  become: yes
  roles:
    - role: justin_p.chisel
```

### Server with example template

```yml
---
- hosts: local
  become: yes
  roles:
    - role: justin_p.chisel
      vars:
        chisel_service_name: chisel-server
        chisel_config_name: chisel-server
```

## Local Development

This role includes molecule that will spin up a local docker environment to deploy, configure and test this role.

Development requirements:

- Docker
- Molecule
- yamllint
- ansible-lint

or simply use a VM with [this](https://github.com/justin-p/ansible-terraform-workstation) configuration.

## License

MIT

## Authors

Justin Perdok ([@justin-p](https://github.com/justin-p/)), Orange Cyberdefense

## Contributing

Feel free to open issues, contribute and submit your Pull Requests. You can also ping me on Twitter ([@JustinPerdok](https://twitter.com/JustinPerdok))
