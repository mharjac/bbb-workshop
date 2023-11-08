# LXD Cheat Sheet

## Table of Contents:

[lxd](#lxd)  
[lxc config](#lxc-config)  
[lxc delete](#lxc-delete)  
[lxc snapshot](#lxc-snapshot)  
[lxc restore](#lxc-restore)  
[lxc exec](#lxc-exec)  
[lxc file](#lxc-file)  
[lxc image](#lxc-image)  
[lxc info](#lxc-info)  
[lxc launch](#lxc-launch)  
[lxc init](#lxc-init)  
[lxc list](#lxc-list)  
[lxc start](#lxc-start)  
[lxc stop](#lxc-stop)  
[lxc restart](#lxc-restart)  
[lxc network](#lxc-network)  
[lxc profile](#lxc-profile)  
[lxc storage](#lxc-storage)  
[lxc publish](#lxc-publish)  
[lxc remote](#lxc-remote)  
[lxc monitor](#lxc-monitor)  
[lxc query](#lxc-query)  
[lxc move](#lxc-move)  
[Misc.](#misc.)  
[Links](#links)  
[Troubleshooting](#troubleshooting)  

## lxd

#### Start initial configuration:

`lxd init`

#### Dump local database:

`lxd sql local .dump`

##### [Table of Contents](#table-of-contents)

## lxc config

#### Edit server config as a YAML file:

`lxc config edit`

#### Edit container config as a YAML file:

`lxc config edit cont1`

#### Change trust password:

`lxc config set core.trust_password password123`

#### Change privilege of a container:

`lxc config set cont1 security.privileged true`

#### Bind folder to a container:

`lxc config device add cont1 shareName disk source=/home/$USER path=/home/ubuntu`

#### Get configuration key:

`lxc config get cont1 limits.processes`

#### Passthrough a network interface to a container:

`lxc config device add cont1 eth0 nic nictype=physical parent=eth1 name=eth0`

#### Add proxy device to a container:

`lxc config device add cont1 dev_name proxy listen=tcp:0.0.0.0:80 connect=tcp:localhost:80`

#### Show container metadata:

`lxc config metadata show cont1`

#### Show templates used by a container:

`lxc config template list cont1`

#### Show trusted clients:

`lxc config trust list`

##### [Table of Contents](#table-of-contents)

## lxc delete

#### Delete a container:

`lxc delete cont1 -f`

#### Delete a snapshot:

`lxc delete cont1/snap1`

##### [Table of Contents](#table-of-contents)

## lxc snapshot

#### Create a snapshot:

`lxc snapshot cont1 snap1`

##### [Table of Contents](#table-of-contents)

## lxc restore

#### Restore from a snapshot:

`lxc restore cont1 snap1`

##### [Table of Contents](#table-of-contents)

## lxc exec

#### Run a command in a container:

`lxc exec cont1 -- /bin/bash`

#### Run a command in a conatiner on a remote server:

`lxc exec host1:cont1 -- apt-get update`

##### [Table of Contents](#table-of-contents)

## lxc file

#### Edit file in a container:

`lxc file edit cont1/file/path/file1`

#### Delete a file in a container:

`lxc file delete cont1/file/path/file1`

#### Push a file to a container:

`lxc file push hosts cont1/tmp/`

#### Pull a file from a container:

`lxc file pull cont1/file/path/file1 .`

##### [Table of Contents](#table-of-contents)

## lxc image

#### Copy an image between servers:

`lxc image copy ubuntu:16.04 local: --alias ubuntu-xenial`

#### List images on a remote server

`lxc image list ubuntu:`

#### List local images:

`lxc image list`

#### Show image info:

`lxc image info bf49cef91a41`

#### Show image properties:

`lxc image show bf49cef91a41`

#### Edit image properties:

`lxc image edit bf49cef91a41`

#### Export an image:

`lxc image export ubuntu:18.04`

##### [Table of Contents](#table-of-contents)

## lxc info

#### Show server/cluster info:

`lxc info`

#### Show container info:

`lxc info cont1`

#### Show last 100 log lines:

`lxc info cont1 --show-log`

##### [Table of Contents](#table-of-contents)

## lxc launch

#### Launch a new container:

`lxc launch ubuntu:18.04 cont1`

#### Launch a cloud instance:

`lxc launch --type aws:m1.large ubuntu:18.04`

#### Launch a temporary container:

`lxc launch ubuntu:18.04 tmp-cont1 --ephemeral`

##### [Table of Contents](#table-of-contents)

### lxc init

#### Create a new container (doesn't start it):

`lxc init ubuntu:18.04 cont1`

##### [Table of Contents](#table-of-contents)

## lxc list

#### List containers:

`lxc list -c n,volatile.base_image:"BASE IMAGE":0,s46,volatile.eth0.hwaddr:MAC`

##### [Table of Contents](#table-of-contents)

## lxc start

#### Start a container:

`lxc start cont1`

#### Start all containers:

`lxc start --all`

##### [Table of Contents](#table-of-contents)

## lxc stop

#### Stop a container:

`lxc stop cont1`

#### Stop all containers:

`lxc stop --all`

#### Kill a container:

`lxc stop cont1 -f`

##### [Table of Contents](#table-of-contents)

## lxc restart

#### Restart a container:

`lxc restart cont1`

#### Restart all containers:

`lxc restart --all`

#### Force container restart:

`lxc restart cont1 -f`

##### [Table of Contents](#table-of-contents)

## lxc network

#### List networks:

`lxc network list`

#### Create a new network (bridge):

`lxc network create lxdbr1`

#### Show information about a network:

`lxc network info lxdbr1`\
`lxc netwokr show lxdbr1`

#### Attach a container to a network:

`lxc network attach lxdbr1 cont1`

#### Show DHCP leases:

`lxc network list-leases lxdbr3`

#### Attach a network interface to a profile:

`lxc network attach-profile lxdbr3 profile1`

##### [Table of Contents](#table-of-contents)

## lxc profile

#### Create a new profile:

`lxc profile create profile-1`

#### Show profile configuration:

`lxc profile show profile-1`

#### Assign profiles to a container:

`lxc profile assign cont1 default,profile1,profile2`

#### Add a profile to a container:

`lxc add cont1 profile2`

#### Copy a profile:

\`lxc profile copy profile1 profile3

#### List devices in a profile:

`lxc profile device list`

#### Add device to a profile:

`lxc profile device add profileName shareName disk source=/home/$USER path=/home/ubuntu`

##### [Table of Contents](#table-of-contents)

## lxc storage

#### Create a new storage:

`lxc storage create lxd_pool4 zfs size=25GB`

#### Show storage configuration:

`lxc storage show default`

#### Show volumes:

`lxc storage volume list pool1`

#### Create a new volume:

`lxc storage volume create lxd_pool vol1 size=10GB`

#### Attach a volume to a container:

`lxc storage volume attach pool1 vol1 cont2 /vol1`

##### [Table of Contents](#table-of-contents)

## lxc publish

#### Create an image from a container:

`lxc publish cont1 --alias testimg1`

##### [Table of Contents](#table-of-contents)

## lxc remote

#### Add a new remote server:

`lxc remote add lxd-host1 10.11.11.3`

#### Show default remote server:

`lxc remote get-default`

##### [Table of Contents](#table-of-contents)

### lxc monitor

#### Monitor LXD server (API calls):

`lxc monitor --pretty`

##### [Table of Contents](#table-of-contents)

### lxc query

#### Send raw API request:

`lxc query -X DELETE --wait /1.0/containers/cont1`

##### [Table of Contents](#table-of-contents)

### lxc move

#### Move a container between storege pools:

`lxc move local:test3 local:test3-1 -s lxd_pool2`

##### [Table of Contents](#table-of-contents)

## Misc.

#### NAT external traffic to a container:

`iptables -t nat -A PREROUTING -i ens160 -p TCP -d 10.66.0.111 --dport 80 -j DNAT --to-destination 10.193.242.81:80`

##### [Table of Contents](#table-of-contents)

## Links

[Getting started with LXD](https://stgraber.org/2015/04/21/lxd-getting-started/)
[dustinkirkland/instance-type](https://github.com/dustinkirkland/instance-type)
[LXD 2.0: Your first LXD container [3/12]](https://blog.ubuntu.com/2016/03/22/lxd-2-0-your-first-lxd-container)
[System container image builder for LXC and LXD](https://github.com/lxc/distrobuilder)
[On the road to lean infrastructure](https://blog.ubuntu.com/2018/04/13/on-the-road-to-lean-infrastructure)
[Server configuration](https://lxd.readthedocs.io/en/latest/server/)
[Container configuration](https://lxd.readthedocs.io/en/latest/containers/)
[Network configuration](https://lxd.readthedocs.io/en/latest/networks/)
[Storage configuration](https://lxd.readthedocs.io/en/latest/storage/)
[LXD, ZFS and bridged networking on Ubuntu 16.04 LTS+](https://bayton.org/docs/linux/lxd/lxd-zfs-and-bridged-networking-on-ubuntu-16-04-lts/)
[LXD Clustering: issues with container failover with node failure](https://discuss.linuxcontainers.org/t/lxd-clustering-issues-with-container-failover-with-node-failure/2168)
[Basic questions about LXD cluster](https://discuss.linuxcontainers.org/t/basic-questions-about-lxd-cluster/1791)
[How to make your LXD containers get IP addresses from your LAN using macvlan](https://blog.simos.info/how-to-make-your-lxd-container-get-ip-addresses-from-your-lan/)
[Help for LXD cluster network](https://discuss.linuxcontainers.org/t/help-for-lxd-cluster-network/1572)
[Turning physical systems into containers Migrating to system containers](https://www.youtube.com/watch?v=JKztAWZOj9g)
[How to migrate LXD from DEB/PPA package to Snap package](https://blog.simos.info/how-to-migrate-lxd-from-deb-ppa-package-to-snap-package/)
[LXD 2.0: Live migration [9/12]](https://stgraber.org/2016/04/25/lxd-2-0-live-migration-912/)
[Container security notes](https://gist.github.com/FrankSpierings/5c79523ba693aaa38bc963083f48456c)
[Trying out LXD containers on Ubuntu on DigitalOcean](https://blog.simos.info/trying-out-lxd-containers-on-ubuntu-on-digitalocean/) [Move container from one pool to another](https://discuss.linuxcontainers.org/t/move-container-from-one-pool-to-another/1296)
[Automatically import your public SSH keys into LXD Instances](http://blog.dustinkirkland.com/2017/02/howto-automatically-import-your-public.html)
[Run graphics-accelerated GUI apps in LXD](https://blog.simos.info/how-to-easily-run-graphics-accelerated-gui-apps-in-lxd-containers-on-your-ubuntu-desktop/)
[Using LXD remote with ssh port forward](http://diogocduarte.github.io/using-lxd-tunnel-ssh.html)
[Managing LXD containers on remote machines](https://www.reddit.com/r/ansible/comments/9b03l8/managing_lxd_containers_on_remote_machines/)
[LXD-P2C does not copy the www folder - different mountpoint](https://github.com/lxc/lxd/issues/5424)

##### [Table of Contents](#table-of-contents)

### Troubleshooting

[Error in live migration](https://discuss.linuxcontainers.org/t/error-in-live-migration/1928)
[LXD ZFS mount empty](https://discuss.linuxcontainers.org/t/lxd-zfs-mount-empty/831)
[Cannot delete LXD zfs backed containers: dataset is busy](https://github.com/lxc/lxd/issues/4656)
[Reclaim Unused Space from /var/lib/lxd/zfs.img?](https://discuss.linuxcontainers.org/t/reclaim-unused-space-from-var-lib-lxd-zfs-img/338)
[tcpdump in unprivileged container: unable to write to stdout/stderr](https://github.com/lxc/lxd/issues/2930)
[Running snaps in LXD unprivileged containers](https://discuss.linuxcontainers.org/t/this-is-cool-running-snaps-in-lxd-unprivileged-containers/1080)
[LXD import not working](https://discuss.linuxcontainers.org/t/lxd-import-not-working/6702) 
[Minimum requirement for lxd-p2c](https://discuss.linuxcontainers.org/t/minimum-requirement-for-lxd-p2c/1687)  

##### [Table of Contents](#table-of-contents)
