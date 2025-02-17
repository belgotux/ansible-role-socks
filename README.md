Proxy
=========

Install danted and add some iptables ssh open ports

Requirements
------------

None

Role Variables
--------------

### Needed variables : 
- `proxy_socks_port`: list of ports for danted-server socks (default `[8008]`)
- `proxy_socks_users`: list of name and passphrase to create proxy ONLY user example :
```
  - name: default_user_proxy_socks
    passhash: $y$yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
```
- `proxy_socks_port_ssh` : original port of the ssh service (default `22`)
- `proxy_socks_ssh_script`: location for the startup script (default `/usr/local/sbin/iptables-ssh.sh`)
- `proxy_socks_second_ports_ssh`: list of ports redirect to SSH original port (default [2222,465])
- `proxy_socks_public_interface`: public interface to listen for second ports ssh (default `eth0`)
- `proxy_socks_ufw`: indicate if ufw rule need to be add (default `false`)

Example Playbook
----------------

```
- hosts: vps.yourdomain.tld

  roles:
    - role: socks
      become: true
      vars: 
        proxy_socks_public_interface: enp0s8
        proxy_socks_second_ports_ssh:
          - 2222
          - 143
          - 465
          - 993
        proxy_socks_port: 8008
        proxy_socks_users:
          - name: user1
            passhash: $y$yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
          - name: user2
            passhash: $y$yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
        proxy_socks_ufw: true
```

License
-------

[GPL v3](https://www.gnu.org/licenses/gpl-3.0.en.html)

Author Information
------------------

Belgotux
[MonLinux](https://www.monlinux.net)