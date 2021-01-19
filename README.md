# This repository will guide you on how to create a MySQL and 2 Websites within a Vagrantfile.


## Pre-Requirements

1. Install the latest version of [Vagrant](https://www.vagrantup.com/docs/installation)

2. Install [VirtualBox](https://www.virtualbox.org/)

## Clone this Repository

```
# git clone https://github.com/dlavric/VagrantTestMysqlWebsite
# cd VagrantTestMysqlWebsite
```

## Whats included?

A `Vagrantfile` that includes 2 webservers and MySQL

'Vagrantfile' from this repository:
```ruby
Vagrant.configure("2") do |config|
 config.vm.box = "anhdht/mysql"
 config.vm.box_version = "0.0.1"


 (1..2).each do |i|
   config.vm.define "web#{i}" do |web|
     web.vm.network "private_network", ip: "192.168.50.#{i+10}" 
     #install webserver
     web.vm.provision "shell", inline: "apt-get update ; apt-get install -y nginx"

end
end
end
```

## Start the VMs

```
# vagrant up
```

## Access the VMs

- Web1
```
# vagrant ssh web1
```

- Web 2
```
# vagrant ssh web2
```
## Connect to the Web VMs

- We need the IPs to connect to the website.

- The IPs are defined in the Vagrantfile
  
  These are the IPs:
```
 Web1 IP: inet 192.168.50.11
 
 Web2 IP: inet 192.168.50.12
```

- We can also find out the IPs with the Linux command `ip addr show` 

```shell
vagrant@myhost:~$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:14:75 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 70875sec preferred_lft 70875sec
    inet6 fe80::a00:27ff:febb:1475/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1a:cb:ca brd ff:ff:ff:ff:ff:ff
    inet 192.168.50.11/24 brd 192.168.50.255 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe1a:cbca/64 scope link 
       valid_lft forever preferred_lft forever
```


- Connect to the Website

Go to your browser and paste the following:

Web 1: http://192.168.50.11
![Screenshot](https://raw.githubusercontent.com/dlavric/VagrantTest/main/Screenshot%202021-01-14%20at%2017.10.47.png)

Web 2: http://192.168.50.12
![Screenshot](https://raw.githubusercontent.com/dlavric/VagrantTest/main/Screenshot%202021-01-14%20at%2017.10.33.png)

