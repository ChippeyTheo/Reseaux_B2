# TP4 INFRA : Router-on-a-stick

## I. Topo 1 : VLAN et Routing

**🌞 Adressage**

```shell
[theo@localhost ~]$ ip a

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:b0:35 brd ff:ff:ff:ff:ff:ff
    inet 10.1.30.1/24 brd 10.1.30.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:febb:b035/64 scope link 
       valid_lft forever preferred_lft forever

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.10.1/24


PC2> show ip 

NAME        : PC2[1]
IP/MASK     : 10.1.10.2/24


adm1> show ip 

NAME        : adm1[1]
IP/MASK     : 10.1.20.1/24
```

**🌞 Configuration des VLANs**

```shell
IOU1#show vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                                Et3/0, Et3/1, Et3/2, Et3/3
10   clients                          active    Et0/1, Et0/2
20   admins                           active    Et0/3
30   servers                          active    Et1/0
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 
```

**🌞 Config du routeur**

```shell
R1#sh ip int br 
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up      
FastEthernet0/0.10         10.1.10.254     YES manual up                    up      
FastEthernet0/0.20         10.1.20.254     YES manual up                    up      
FastEthernet0/0.30         10.1.30.254     YES manual up                    up   
```

**🌞 Vérif**

```shell
[theo@localhost ~]$ ping 10.1.30.254
PING 10.1.30.254 (10.1.30.254) 56(84) bytes of data.
64 bytes from 10.1.30.254: icmp_seq=1 ttl=255 time=16.6 ms
64 bytes from 10.1.30.254: icmp_seq=2 ttl=255 time=3.25 ms
64 bytes from 10.1.30.254: icmp_seq=3 ttl=255 time=11.3 ms
64 bytes from 10.1.30.254: icmp_seq=4 ttl=255 time=5.36 ms


PC2> ping 10.1.10.254

10.1.10.254 icmp_seq=1 timeout
84 bytes from 10.1.10.254 icmp_seq=2 ttl=255 time=4.061 ms
84 bytes from 10.1.10.254 icmp_seq=3 ttl=255 time=2.277 ms


PC1> ping 10.1.10.254

10.1.10.254 icmp_seq=1 timeout
84 bytes from 10.1.10.254 icmp_seq=2 ttl=255 time=7.441 ms
84 bytes from 10.1.10.254 icmp_seq=3 ttl=255 time=9.921 ms
84 bytes from 10.1.10.254 icmp_seq=4 ttl=255 time=11.451 ms


adm1> ping 10.1.20.254

10.1.20.254 icmp_seq=1 timeout
84 bytes from 10.1.20.254 icmp_seq=2 ttl=255 time=6.539 ms
84 bytes from 10.1.20.254 icmp_seq=3 ttl=255 time=5.390 ms
```


```shell
[theo@localhost ~]$ ping 10.1.10.1
PING 10.1.10.1 (10.1.10.1) 56(84) bytes of data.
64 bytes from 10.1.10.1: icmp_seq=1 ttl=63 time=32.5 ms
64 bytes from 10.1.10.1: icmp_seq=2 ttl=63 time=15.4 ms


adm1> ping 10.1.10.2

84 bytes from 10.1.10.2 icmp_seq=1 ttl=63 time=30.935 ms
84 bytes from 10.1.10.2 icmp_seq=2 ttl=63 time=17.126 ms
```

## II. NAT

**🌞 Ajoutez le noeud Cloud à la topo**

```shell
R1#sh ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up      
FastEthernet0/0.10         10.1.10.254     YES manual up                    up      
FastEthernet0/0.20         10.1.20.254     YES manual up                    up      
FastEthernet0/0.30         10.1.30.254     YES manual up                    up      
FastEthernet1/0            10.0.3.16       YES DHCP   up                    up      
FastEthernet1/1            unassigned      YES unset  administratively down down    
FastEthernet2/0            unassigned      YES unset  administratively down down    
FastEthernet2/1            unassigned      YES unset  administratively down down    


R1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 56/60/64 ms
```

**🌞 Configurez le NAT**

```shell
R1#conf t
R1(config)#interface f
R1(config)#interface fastEthernet 1/0
R1(config-if)#ip nat outside
R1(config-if)#exit
R1(config)#interface fastEthernet 0/0
R1(config-if)#ip nat inside
R1(config-if)#exit
R1(config)#ip nat inside source list 1 interface fastEthernet 1/0 overload
R1(config)#exit
```

**🌞 Test**

```shell
[theo@localhost ~]$ ping google.com
PING google.com (142.250.201.46) 56(84) bytes of data.
64 bytes from mrs08s20-in-f14.1e100.net (142.250.201.46): icmp_seq=1 ttl=61 time=29.9 ms
64 bytes from mrs08s20-in-f14.1e100.net (142.250.201.46): icmp_seq=2 ttl=61 time=30.3 ms
64 bytes from mrs08s20-in-f14.1e100.net (142.250.201.46): icmp_seq=3 ttl=61 time=47.6 ms


PC1> ping google.com
google.com resolved to 142.251.37.46

84 bytes from 142.251.37.46 icmp_seq=1 ttl=61 time=30.056 ms
84 bytes from 142.251.37.46 icmp_seq=2 ttl=61 time=26.616 ms


adm1> ping google.com
google.com resolved to 142.250.200.206

84 bytes from 142.250.200.206 icmp_seq=1 ttl=61 time=32.008 ms
84 bytes from 142.250.200.206 icmp_seq=2 ttl=61 time=26.142 ms
84 bytes from 142.250.200.206 icmp_seq=3 ttl=61 time=34.116 ms


PC2> ping google.com
google.com resolved to 142.250.201.46

84 bytes from 142.250.201.46 icmp_seq=1 ttl=61 time=42.089 ms
84 bytes from 142.250.201.46 icmp_seq=2 ttl=61 time=38.807 ms
```

## III. Add a building

**🌞  Vous devez me rendre le show running-config de tous les équipements**

- [routeur](/TP4/routeur.md)
- [switch_1](/TP4/switch1.md)
- [switch_2](/TP4/switch2.md)
- [switch_3](/TP4/switch3.md)

**🌞  Mettre en place un serveur DHCP dans le nouveau bâtiment**

```shell
PC4> ip dhcp
DDORA IP 10.1.10.11/24 GW 10.1.10.254

PC4> sh ip

NAME        : PC4[1]
IP/MASK     : 10.1.10.11/24
GATEWAY     : 10.1.10.254
DNS         : 1.1.1.1  
DHCP SERVER : 10.1.10.253
DHCP LEASE  : 897, 900/450/787
MAC         : 00:50:79:66:68:04
LPORT       : 20035
RHOST:PORT  : 127.0.0.1:20036
MTU         : 1500

PC4> ping 10.1.10.1

84 bytes from 10.1.10.1 icmp_seq=1 ttl=64 time=2.492 ms
84 bytes from 10.1.10.1 icmp_seq=2 ttl=64 time=3.176 ms
^C
PC4> ping 10.1.30.1

84 bytes from 10.1.30.1 icmp_seq=1 ttl=63 time=18.843 ms
84 bytes from 10.1.30.1 icmp_seq=2 ttl=63 time=18.966 ms
^C
PC4> ping 10.1.10.253

84 bytes from 10.1.10.253 icmp_seq=1 ttl=64 time=1.728 ms
84 bytes from 10.1.10.253 icmp_seq=2 ttl=64 time=1.869 ms
^C
PC4> ping 10.1.10.254

84 bytes from 10.1.10.254 icmp_seq=1 ttl=255 time=10.799 ms
84 bytes from 10.1.10.254 icmp_seq=2 ttl=255 time=9.576 ms
^C
```

**🌞  Vérification**

```shell
PC3> ip dhcp
DDORA IP 10.1.10.10/24 GW 10.1.10.254

PC3> sh ip 

NAME        : PC3[1]
IP/MASK     : 10.1.10.10/24
GATEWAY     : 10.1.10.254
DNS         : 1.1.1.1  
DHCP SERVER : 10.1.10.253
DHCP LEASE  : 896, 900/450/787
MAC         : 00:50:79:66:68:03
LPORT       : 20033
RHOST:PORT  : 127.0.0.1:20034
MTU         : 1500

PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=59 time=30.492 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=59 time=25.894 ms
^C
PC3> ping google.com
google.com resolved to 142.250.200.238

84 bytes from 142.250.200.238 icmp_seq=1 ttl=59 time=31.581 ms
84 bytes from 142.250.200.238 icmp_seq=2 ttl=59 time=28.806 ms
84 bytes from 142.250.200.238 icmp_seq=3 ttl=59 time=26.321 ms
```