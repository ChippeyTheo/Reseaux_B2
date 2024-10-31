# TP6 INFRA : STP, OSPF, bigger infra

## I. STP

### 1. Basic setup

**🌞 Configurer STP sur les 3 switches**

```shell
IOU3#sh spanning-tree 

VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     aabb.cc00.0100
             Cost        100
             Port        1 (Ethernet0/0)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.0300
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Root FWD 100       128.1    P2p 
Et0/1               Altn BLK 100       128.2    P2p 
Et0/2               Desg FWD 100       128.3    P2p 
Et0/3               Desg FWD 100       128.4    P2p 
```

**🌞 Altérer le spanning-tree en désactivant un port**

```shell
IOU3#sh spanning-tree     

VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     aabb.cc00.0100
             Cost        200
             Port        2 (Ethernet0/1)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.0300
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  15  sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Root LIS 100       128.2    P2p 
Et0/2               Desg FWD 100       128.3    P2p 
Et0/3               Desg FWD 100       128.4    P2p 
```

**🌞 Altérer le spanning-tree en modifiant le coût d'un lien**

```shell
IOU3#sh spanning-tree 

VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     aabb.cc00.0100
             Cost        200
             Port        2 (Ethernet0/1)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.0300
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  15  sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Altn BLK 500       128.1    P2p 
Et0/1               Root LIS 100       128.2    P2p 
Et0/2               Desg FWD 100       128.3    P2p 
Et0/3               Desg FWD 100       128.4    P2p 
```

**🦈 tp6_stp.pcapng**

- [capture stp](/TP6/tp6_stp.pcapng)

### 2. Fonctionnalités avancées

- [lien vers explication en ligne](https://www.formip.com/pages/blog/portfast-et-bpdu-guard)


bpduguard l'activer sur les ports qui ne lient pas un switch protege des pc qui veulent se faire passer pour un switch

## II. OSPF

**🌞 Montez la topologie**

- [routeur1](/TP6/routeur1.md)
- [routeur2](/TP6/routeur2.md)
- [routeur3](/TP6/routeur3.md)
- [routeur4](/TP6/routeur4.md)
- [routeur5](/TP6/routeur5.md)

- ping R2 a R1
```shell
R2#ping 10.6.12.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.6.12.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 60/61/64 ms
```

- ping meow a R4
```shell
meow> ping 10.6.2.254

84 bytes from 10.6.2.254 icmp_seq=1 ttl=255 time=19.440 ms
84 bytes from 10.6.2.254 icmp_seq=2 ttl=255 time=9.471 ms
84 bytes from 10.6.2.254 icmp_seq=3 ttl=255 time=9.634 ms
84 bytes from 10.6.2.254 icmp_seq=4 ttl=255 time=6.582 ms
84 bytes from 10.6.2.254 icmp_seq=5 ttl=255 time=9.374 ms
```

- ping john a R1
```shell
john> ping 10.6.3.254

84 bytes from 10.6.3.254 icmp_seq=1 ttl=255 time=10.006 ms
84 bytes from 10.6.3.254 icmp_seq=2 ttl=255 time=7.917 ms
84 bytes from 10.6.3.254 icmp_seq=3 ttl=255 time=6.261 ms
84 bytes from 10.6.3.254 icmp_seq=4 ttl=255 time=8.635 ms
84 bytes from 10.6.3.254 icmp_seq=5 ttl=255 time=7.442 ms
```

- ping R5 internet
```shell
R5#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 60/61/64 ms
```

**🌞 Configurer OSPF sur tous les routeurs**

- [routeur1](/TP6/routeur1_ospf.md)

- [routeur2](/TP6/routeur2_ospf.md)
- [routeur3](/TP6/routeur3_ospf.md)
- [routeur4](/TP6/routeur4_ospf.md)
- [routeur5](/TP6/routeur5_ospf.md)


**🌞 Test**

```shell
waf> ping 10.6.3.11

84 bytes from 10.6.3.11 icmp_seq=1 ttl=62 time=49.963 ms
84 bytes from 10.6.3.11 icmp_seq=2 ttl=62 time=35.914 ms
84 bytes from 10.6.3.11 icmp_seq=3 ttl=62 time=31.774 ms
84 bytes from 10.6.3.11 icmp_seq=4 ttl=62 time=25.306 ms

meow> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=53 time=83.567 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=53 time=68.788 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=53 time=89.137 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=53 time=68.642 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=53 time=63.600 ms

R1#ping 1.1.1.1  

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 44/48/52 ms
```

**🦈 tp6_ospf.pcapng**

- [capture ospf](/TP6/tp6_ospf.pcapng)

## III. DHCP relay

**🌞 Configurer un serveur DHCP sur dhcp.tp6.b1**

```shell
[theo@localhost ~]$ sudo cat /etc/dhcp/dhcpd.conf
#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#

default-lease-time 600;

max-lease-time 7200;

authoritative;

subnet 10.6.1.0 netmask 255.255.255.0 {
range 10.6.1.100 10.6.1.200;
option broadcast-address 10.6.1.255;
option routers 10.6.1.254;
option domain-name-servers 1.1.1.1;
}

subnet 10.6.3.0 netmask 255.255.255.0 {
range 10.6.3.100 10.6.3.200;
option broadcast-address 10.6.3.255;
option routers 10.6.3.254;
option domain-name-servers 1.1.1.1;
}
```

```shell
[theo@localhost ~]$ sudo systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: di>
     Active: active (running) since Thu 2024-10-31 14:58:39 CET; 2min 27s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 11486 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 4672)
     Memory: 5.3M
        CPU: 12ms
     CGroup: /system.slice/dhcpd.service
             └─11486 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -g>

Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: ** Ignoring requests on enp>
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    you want, please write a>
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    in your dhcpd.conf file >
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    to which interface enp0s>
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: 
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Listening on LPF/enp0s3/08:>
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Sending on   LPF/enp0s3/08:>
lines 1-20...skipping...
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Thu 2024-10-31 14:58:39 CET; 2min 27s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 11486 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 4672)
     Memory: 5.3M
        CPU: 12ms
     CGroup: /system.slice/dhcpd.service
             └─11486 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid

Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: ** Ignoring requests on enp0s8.  If this is not what
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    you want, please write a subnet declaration
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    in your dhcpd.conf file for the network segment
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]:    to which interface enp0s8 is attached. **
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: 
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Listening on LPF/enp0s3/08:00:27:fc:07:db/10.6.1.0/24
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Sending on   LPF/enp0s3/08:00:27:fc:07:db/10.6.1.0/24
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Sending on   Socket/fallback/fallback-net
Oct 31 14:58:39 localhost.localdomain dhcpd[11486]: Server starting service.
Oct 31 14:58:39 localhost.localdomain systemd[1]: Started DHCPv4 Server Daemon.
```

**🌞 Configurer un DHCP relay sur la passerelle de John**

```shell
waf> ip dhcp
DDORA IP 10.6.1.100/24 GW 10.6.1.254
```