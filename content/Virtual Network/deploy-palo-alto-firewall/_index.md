---
title: "How to Deploy Palo Alto Firewall"
date: 2020-9-29T11:02:05+06:00
weight: 4
draft: false
---

The applications and data in the cloud need to be protected, Paloalto VM-Series firewall protects your cloud workload by inspecting the traffic going in and out of the virtual environment. Cloud Security refers to a broad set of control-based technologies and policies deployed to protect information, data, applications, and infrastructure associated with cloud computing.
There are two deployment modes, Standalone instance or High availability (Active-Active or Active-Passive)

1.Standalone Deployment Procedures:

![Standalone Deployment](https://kb.bluvalt.com/uploads/Picture1-fw.png)

1.1 Create Virtual networks (Outside, Web, APP, DB and management) with the preferred IP schema.

```
openstack subnet create --subnet-range <subnet-range> --gateway auto --dhcp --dns-nameserver <dns-nameserver> --network <network> --host-route destination=<subnet>,gateway=<ip-address> name
```

```
openstack network create Web openstack subnet create --subnet-range 192.168.1.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network Web --dns-nameserver 1.1.1.1 --host-route destination=0.0.0.0/0,gateway=192.168.1.254 Web
```

```openstack network create APP
openstack subnet create --subnet-range 192.168.2.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network APP --dns-nameserver 1.1.1.1 --host-route destination=0.0.0.0/0,gateway=192.168.2.254 APP
```

```
openstack network create DB
openstack subnet create --subnet-range 192.168.3.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network DB --dns-nameserver 1.1.1.1 --host-route destination=0.0.0.0/0,gateway=192.168.3.254 DB
```

```
openstack network create Outside
openstack subnet create --subnet-range 192.168.0.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network Outside  --dns-nameserver 1.1.1.1 --host-route destination=0.0.0.0/0,gateway=192.168.0.254 Outside
```

```
openstack network create Outside
openstack subnet create --subnet-range 192.168.0.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network Outside  --dns-nameserver 1.1.1.1 --host-route destination=0.0.0.0/0,gateway=192.168.0.254 Outside
```

```
openstack network create Mgm
openstack subnet create --subnet-range 10.10.10.0/24 --gateway auto --dhcp --dns-nameserver 46.49.140.155 --network Mgm --dns-nameserver 1.1.1.1 Mgm
```

1.2 Create Logical router, set external gateway, attach Mgm and Outside virtual networks to the router. (From Horizon dashboard)

1.3 Disable RPF (Reverse Pass Forwarding) for each virtual network attached to the firewall instance.

1.4 Deploy the FW instance and attach to each logical network including management network with interface IP. x.x.x.254 (Convert your PAN image to bootable volume first)

```
nova boot --flavor <Flavor-id> --boot-volume <Volume-ID> --nic net-id=<Mgm-net-id>,v4-fixed-ip=10.10.10.10  --nic net-id=<Web-net-id>,v4-fixed-ip=192.168.1.254 --nic net-id=<APP-net-id>,v4-fixed-ip=192.168.2.254  --nic net-id=<DB-net-id>,v4-fixed-ip=192.168.3.254   --nic net-id=<Outside-net-id>,v4-fixed-ip=192.168.0.254   FW-Name
```

1.5 Define the security group on the FW instance which allow all incoming traffic. (From Horizon dashboard)

1.6 Associate Floating IP to the FW Instance management interface. (From Horizon dashboard)

1.7 Make sure the Firewall instance is reachable from any browser using https://Floating-IP

1.8 Change the default password to secured one.

1.9 From Firewall Command line interface, make sure your instance can reach internet using management interface for Paloalto update servers.

1.10 Define DNS in your firewall instance.

1.11 Create management profile with ICMP allowed and assigned to your interfaces

1.12 Update your Firewall instance.

1.13 Disable DPDK inside your firewall instance and reboot.

```
show system setting dpdk-pkt-io
set system setting dpdk-pkt-io off
```

_request restart system_

1.14 Set your interface mode in DHCP inside your firewall instance, make sure you have received the correct DHCP IP Address from openstack overlay network DHCP Server.

1.15 Change DHCP mode to static IP configuration, create the required security zones (Outside, Web, APP, DB)

1.16 Define the default route by creating static route 0.0.0.0 next hop 192.168.0.1

1.17 From Firewall instance, make sure you can reach internet using your Outside interface IP

1.18 Define the security policy to allow the required traffic type

1.19 Define NAT rule to allow internet traffic to your VMs which not associated with Floating IP.

1.20 If you need to publish services to public such as Exchange, Web sites, ftp …etc, Follow the following steps

![Allow Address Pair](https://kb.bluvalt.com/uploads/Picture2-fw2.png)

Define ‘allow address pairs’ with IP 192.168.0.10 on the outside interface of your firewall instance by updating the neutron port using the following cli command:

```
neutron port-update `<FW-Outside-port-id>` --allowed_address_pairs list=true type=dict ip_address=192.168.0.10
```

Associate Floating IP address to the VIP to publish the service to public access using the following Openstack CLI command:

```
neutron floatingip-associate --fixed-ip-address 192.168.0.10 FLOATINGIP_ID FW-Outside-PORT_ID
```

1.21 Define NAT policy inside your Firewall instance – Static NAT/Bidirectional.

1.22 Configure The VIP ’192.168.0.10’ on the outside interface as a secondary IP inside Firewall instance Dashboard.

1.23 Make sure your exchange VM has the default GW to your firewall instance and it is reachable.

For details, see our technical video for PAN deployment on openstack from the following link:

[Palo Alto Deployment - Video Tutorial](https://www.youtube.com/watch?v=e6ydyAj1ai8&feature=youtu.be)
