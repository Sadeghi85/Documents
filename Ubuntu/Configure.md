
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
- set timezone
```
$ ln -sf /usr/share/zoneinfo/Asia/Tehran /etc/localtime
```
---
- set date
> check: `$ date` & `$ hwclock`
```
$ date MMDDhhmm
$ hwclock -w
```
---
- package management
```
$ apt install nmap
$ apt remove nmap
$ apt update && apt dist-upgrade
```
> to list all packages in the system’s package database
```
$ dpkg -l | grep apache2
```
> to list the files installed by a package, in this case the ufw package, enter:
```
$ dpkg -L ufw
```
> if you are not sure which package installed a file, `dpkg -S` may be able to tell you
```
$ dpkg -S /etc/host.conf
```
> you can install a local `.deb` file by entering:
```
$ dpkg -i zip_3.0-4_amd64.deb
```
> uninstalling a package can be accomplished by:
```
$ dpkg -r zip
```
> configuration of the _Advanced Packaging Tool_ (APT) system repositories is stored in the `/etc/apt/sources.list` file and the `/etc/apt/sources.list.d` directory
---