


# Configuring Ubuntu

- find interface name
```
$ ip address show
```
- routes
```
$ ip route
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
```
> to update packages
```
$ apt update && apt dist-upgrade
```
> to search packages
```
$ apt-cache search keyword
```
> to check version of packages
```
$ apt list -a keyword
or
$ apt-cache policy keyword
```
> to install specific version of package
```
$ apt install redis=6:6.2.6-3rl1~focal1
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
- disable `root` account
```
$ useradd -m -s $(which bash) -G sudo poweruser
$ passwd poweruser
```
```
$ visudo

[...]
	#%sudo  ALL=(ALL:ALL) ALL
	%sudo ALL=(ALL) NOPASSWD: ALL

	Defaults:%sudo    !requiretty
[...]
```
```
$ usermod --lock root
```
> now logout and login as the newly created admin account

> description
>
> the newly created admin account is effectively like the root; It can sudo, doesn't need to enter password for sudo and doesn't require tty to login(so you can login as root with WinSCP even though the root account is disabled; under WinSCP advanced option SCP/Shell, choose `sudo su -` as shell), therefore all security concerns about root applies to this account too, except now the attacker needs to also guess the username instead of just brute-forcing root's password.
---
- enable `root` account
> login with an account with sudo permission
```
$ sudo su -
$ passwd
```
```
$ vi /etc/ssh/sshd_config

[...]
	PermitRootLogin yes
[...]
```
```
$ systemctl restart sshd
```
---
- disable ipv6
```
$ vi /etc/default/grub

[...]
	GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disable=1"
[...]
```
```
$ update-grub
```
```
$ reboot
```
---
- useful packages
```
$ apt install htop nmap iftop iotop net-tools bind9-dnsutils
```