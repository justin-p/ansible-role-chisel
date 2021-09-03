# ansible-role-chisel

[![Ansible Role Name](https://img.shields.io/ansible/role/51177?label=Role%20Name&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/chisel)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/51177?label=Ansible%20Quality%20Score&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/chisel)
[![Ansible Role Downloads](https://img.shields.io/ansible/role/d/51177?label=Ansible%20Role%20Downloads&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/chisel)
[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/ansible-role-chisel/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/ansible-role-chisel/actions)

A Ansible role to deploy a [chisel](https://github.com/jpillora/chisel) client and/or server as a systemd service. The main idea is to use this to easly automate a dropbox scenario that ensures the client always callsback regardless of network issues, reboots or program crashes, while also taking advantage of what chisel can offer over a SSH or VPN based solution.

## Requirements

None.

## Variables

`defaults/main.yml`

| Variable                         | Description                                                                                                                                                                                                                                                | Default value                                                                                                             |
| :------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------- |
| chisel_version                   | The release version of chisel linux amd64 to download.                                                                                                                                                                                                     | 1.7.6                                                                                                                     |
| chisel_download_url_linux_amd64  | The download url.                                                                                                                                                                                                                                          | `https:\\github.com/jpillora/chisel/releases/download/v{{ chisel_version }}/chisel\_{{ chisel_version }}\_linux_amd64.gz` |
| chisel_linux_amd64_sha256        | The sha256 checksum of the downloaded file.                                                                                                                                                                                                                | b08782b58eb043e7cd649302ceea993582f55762d7b384c418253d227930fe32                                                          |
| chisel_download_destination      | The download destination.                                                                                                                                                                                                                                  | /tmp/chisel\_{{ chisel_version }}.gz                                                                                      |
| chisel_install_destination       | The location to install chisel.                                                                                                                                                                                                                            | /usr/local/bin/chisel                                                                                                     |
| chisel_service_name              | The name of the service that should be installed.                                                                                                                                                                                                          | chisel-client                                                                                                             |
| chisel_service_destination       | The destination where of the service file should be installed.                                                                                                                                                                                             | "/lib/systemd/system/{{ chisel_service_name }}.service"                                                                   |
| chisel_service_template          | This role has 2 build-in templates, [chisel-client](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-client.service.j2) and [chisel-server](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-server.service.j2). | "{{ chisel_service_name }}.service.j2"                                                                                    |
| chisel_config_name               | The name of the chisel config.                                                                                                                                                                                                                             | chisel-client                                                                                                             |
| chisel_config_folder             | The folder where the chisel config will be installed.                                                                                                                                                                                                      | /etc/chisel/                                                                                                              |
| chisel_config_template           | This role has 2 build-in templates, [chisel-client](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-client.conf.j2) and [chisel-server](https://github.com/justin-p/ansible-chisel/blob/main/templates/chisel-server.conf.j2).       | "{{ chisel_config_name }}.conf.j2"                                                                                        |
| chisel_config_destination        | The full path where the chisel config will be installed.                                                                                                                                                                                                   | "{{ chisel_config_folder }}{{ chisel_config_name }}.conf"                                                                 |
| chisel_client_server_url         | The URL of the chisel server.                                                                                                                                                                                                                              | `http://127.0.0.1`                                                                                                        |
| chisel_client_remotes            | The remotes that are tunneled through the server.                                                                                                                                                                                                          | "8080"                                                                                                                    |
| chisel_client_server_fingerprint | The fingerprint of the server.                                                                                                                                                                                                                             | aa:bb:cc:dd:ee:ff:gg                                                                                                      |
| chisel_client_auth_username      | The username to authenticate with.                                                                                                                                                                                                                         | user                                                                                                                      |
| chisel_client_auth_password      | The password to authenticate with.                                                                                                                                                                                                                         | pass                                                                                                                      |
| chisel_client_keepalive          | The keep alive for the client.                                                                                                                                                                                                                             | 25s                                                                                                                       |
| chisel_client_max_retry_count    | The max retry count for the client.                                                                                                                                                                                                                        | unlimited                                                                                                                 |
| chisel_client_max_retry_interval | The max retry interval for the client.                                                                                                                                                                                                                     | 5                                                                                                                         |
| chisel_client_proxy              | An optional HTTP CONNECT or SOCKS5 proxy which will be used to reach the chisel server.                                                                                                                                                                    | http://admin:password@my-server.com:8081                                                                                  |
| chisel_client_headers            | Set a custom header in the form "HeaderName: HeaderContent".                                                                                                                                                                                               | '--header "Foo : Bar" --header "Hello : World"'                                                                           |
| chisel_client_hostname           | Optionally set the 'Host' header.                                                                                                                                                                                                                          | example.com                                                                                                               |
| chisel_client_tls_ca             | An optional root certificate bundle used to verify the chisel server.                                                                                                                                                                                      | /path/to/bundle                                                                                                           |
| chisel_client_tls_key            | A path to a PEM encoded private key used for client authentication.                                                                                                                                                                                        | /path/to/PEM                                                                                                              |
| chisel_client_tls_cert           | A path to a PEM encoded certificate matching the provided private key.                                                                                                                                                                                     | /path/to/PEM                                                                                                              |
| chisel_server_host               | Defines the HTTP listening host – the network interface.                                                                                                                                                                                                   | 0.0.0.0                                                                                                                   |
| chisel_server_port               | Defines the HTTP listening port.                                                                                                                                                                                                                           | 80                                                                                                                        |
| chisel_server_key                | An optional string to seed the generation of a ECDSA keypair.                                                                                                                                                                                              | a_random_string                                                                                                           |
| chisel_server_auth_file          | An optional path to a users.json file.                                                                                                                                                                                                                     | /path/to/user.json                                                                                                        |
| chisel_server_auth               | An optional string representing a single user with full access.                                                                                                                                                                                            | user:pass                                                                                                                 |
| chisel_server_keepalive          | The keep alive for the server.                                                                                                                                                                                                                             | 25s                                                                                                                       |
| chisel_server_backend            | Specifies another HTTP server to proxy requests to when chisel receives a normal HTTP request.                                                                                                                                                             | http://127.0.0.1:8081                                                                                                     |
| chisel_server_tls_ca             | A path to a PEM encoded CA certificate bundle.                                                                                                                                                                                                             | /path/to/PEM                                                                                                              |
| chisel_server_tls_key            | Enables TLS and provides optional path to a PEM-encoded TLS private key.                                                                                                                                                                                   | /path/to/PEM                                                                                                              |
| chisel_server_tls_cert           | Enables TLS and provides optional path to a PEM-encoded TLS certificate.                                                                                                                                                                                   | /path/to/PEM                                                                                                              |

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
