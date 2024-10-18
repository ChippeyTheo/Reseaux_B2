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

```

