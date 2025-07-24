
# RHCSA/RHCE Lab Environment

NOTE: VM's are empty inside... it's just playground enviroment to train...

---
## Installing prerequisites Vagrant and VirtualBox 
 - [Vagrant_Install] (https://developer.hashicorp.com/vagrant/install)
 - [VirtualBox] (https://download.virtualbox.org/virtualbox/6.1.40/)

### Plugins

>  Please first install this plugins:

```
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-registration

```

### Usage

>  First time it take around 30 min for setup and make essential configurations
>>  Next time vagrant need just a few seconds... 
>>  If all VM are not up in the same time ,run "vagrant up" command again. 

```

# ignition! this command setup or turn on all the machines
#  ** Make sure your are under Vagranfile folder location to run vagrant up command ** 

- vagrant up

# if you make some change on the extras files, to apply it use the flag --provission

- vagrant up --provision

######### the prompt ask you for chose the bridge interface, common cases use **eth0** or the firs available real interface.

######### put the number of your interface and hit enter.

1) Intel(R) Wi-Fi 6 AX200 160MHz
2) Hyper-V Virtual Ethernet Adapter

    bastion: Which interface should the network bridge to? 1

######### my cast I have selected to Intel WiFi

```


### Useful vagrant commands:
> to avoid re-provision over and over again when you want start from a clean instance use `snapshot save` the first time you deploy the lab and `snaphost restore` every single time you want a fresh and quick instance.

```
vagrant destroy -f - Shuts down and destroys the environment
vagrant halt - Shuts down the environment VMs (can be booted up with vagrant up)
vagrant suspend - Puts the VMs in a suspended state
vagrant resume - Takes VMs out of a suspended state

# first time you have the lab up and running save it with a snapshot
vagrant snapshot save base-00

# to list all the saved snapshot
vagrant snapshot list

# to restore a snapshot
vagrant snapshot restore base-00
```
### topology

```
192.168.54.9    bastion        bastion.lab.example.com
192.168.54.10     servera        servera.lab.example.com
192.168.54.11     serverb        serverb.lab.example.com

192.168.54.8     ·······        use this ip for LAN access 
```

### default credentials

```
user: root
pass: redhat

user: student
pass: student

```

### NFS Server setup on bastion host 

``` 
sudo dnf install nfs-utils -y     
sudo systemctl enable --now nfs-server

sudo useradd netuserX
sudo passwd netuserX   # set to ablerate

sudo mkdir -p /home/guests/netuserX
sudo chown netuserX:netuserX /home/guests/netuserX
sudo chmod 700 /home/guests/netuserX
```

sudo nano /etc/exports

```
/home/guests/netuserX  *(rw,sync,no_root_squash)
sudo exportfs -rav

#check export list 
exportfs -v 
```
