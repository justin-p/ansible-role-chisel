# ansible-chisel

## client with example template

```
---
- hosts: local
  become: yes
  roles:
    - role: justin_p.chisel
```

## server with example template

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
