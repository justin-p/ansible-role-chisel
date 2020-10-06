# ansible-chisel

A Ansible role to deploy a chisel client and/or server as a systemd service.

## Variables

| to  | do  |
| --- | --- |
|     |     |

## Examples

### Client with example template

```
---
- hosts: local
  become: yes
  roles:
    - role: justin_p.chisel
```

### Server with example template

```
---
  - hosts: local
    become: yes
    roles:
      - role: justin_p.chisel
        vars:
          chisel_service_name: chisel-server
          chisel_config_name: chisel-server
```

## Contributing

Feel free to open issues, contribute and submit your Pull Requests. You can also ping me on Twitter ([@JustinPerdok](https://twitter.com/JustinPerdok))
