# Configuring Ubuntu

- find interface name
```
$ ip address show
```
---
- set dynamic ip
```
$ vi /etc/netplan/01-ens33-config.yaml
```
```yaml
network:
    version: 2
    ethernets:
        ens33:
            dhcp4: true
```
```
$ netplan apply
```
---
- set static ip
```
$ vi /etc/netplan/01-ens33-config.yaml
```
```yaml
network:
    version: 2
    ethernets:
        ens33:
            addresses: [172.17.105.200/28]
            gateway4: 172.17.105.192
            nameservers:
                addresses: [4.2.2.2, 8.8.8.8]
```
```
$ netplan apply
```
---
- network
```
$ ss -tulpn
```
---
- list services
```
$ systemctl list-unit-files
$ systemctl list-dependencies [target]
```
---
- enable, disable, status, start, stop, restart services
```
$ systemctl status httpd
$ systemctl disable httpd
$ systemctl enable nginx
$ systemctl start php-fpm
$ systemctl restart php-fpm
$ systemctl stop php-fpm
```
---
- hostname
```
$ vi /etc/hosts
```
```
127.0.0.1 localhost
127.0.1.1 openproject
```
```
$ hostnamectl set-hostname openproject --static
$ systemctl restart systemd-hostnamed
```
> both `$ hostname` & `$ hostname -f` should output the same hostname
---