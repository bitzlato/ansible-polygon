# Ansible Role: Matic Mainnet full node 
Install Matic Mainnet Full Node on Debian/Ubuntu servers.

This role installs and configures Heimdall and Bor for  Matic Mainnet Full Node. You will likely need to do extra setup work before this role,  like changing variables, describing the location and options to use for your particular node.

# Requirements
Minimal:
****4 core
8 RAM
2TB of free disk space


Recommended:
****8 core
16 RAM
2TB of free disk space


# Dependencies
golang v1.14.0+

# Role Variables
Available variables are listed below, along with default values (see defaults/main.yml):

```
golang_path: ""
```
Be sure to specify the value of the golang_path variable.

```
bor_branch: "v0.2.14"
```

The branch from the bor repository https://github.com/maticnetwork/bor.git

```
heimdall_rpc_address: "127.0.0.1"
```
TCP or UNIX socket address for the RPC server to listen on Heimdall

```
bor_http_addr: "127.0.0.1"
```
Bor HTTP-RPC server listening interface

# Example Playbook
```
- hosts: node
  become: yes
  vars:
    golang_path: "/opt/go/1.17.6/bin:{{ ansible_env.PATH }}"
  roles:
     - role: roles/ansible-polygon
```

# Launch Polygon node

Heimdall service starts first, wait until Heimdall is synchronized. Check the sync status:

```
curl 127.0.0.1:26657/status
```
catching_up should show_ false_

Next, we start the heimdalld-rest-server service and the bor service
