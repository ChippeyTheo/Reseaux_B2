# TP7 INFRA : 3-tier architecture et redondance

## 1. Présentation archi

### A. Topologie réseau

![shéma de la topologie](/IMG/topologie-tp7.png)

### B. Tableau d'adressage et C. Tableau des VLANs

## 2. Technos utilisées

**🌞 show-run sur tous les équipements**

- [routeur_1](/TP7/CONF/routeur1.md)
- [routeur_2](/TP7/CONF/routeur2.md)
- [switch_1](/TP7/CONF/swt1.md)
- [switch_2](/TP7/CONF/swt2.md)
- [switch_3](/TP7/CONF/swt3.md)
- [switch_4](/TP7/CONF/swt4.md)
- [switch_5](/TP7/CONF/swt5.md)
- [switch_6](/TP7/CONF/swt6.md)
- [switch_7](/TP7/CONF/swt7.md)

**🌞 depuis pc4.tp7.b1**

```shell
PC1> ping 10.7.30.11 #note mon PC1 = PC4 de la topologie donnée

84 bytes from 10.7.30.11 icmp_seq=1 ttl=63 time=15.601 ms
84 bytes from 10.7.30.11 icmp_seq=2 ttl=63 time=14.640 ms
84 bytes from 10.7.30.11 icmp_seq=3 ttl=63 time=23.058 ms
84 bytes from 10.7.30.11 icmp_seq=4 ttl=63 time=23.718 ms
84 bytes from 10.7.30.11 icmp_seq=5 ttl=63 time=19.830 ms

PC1> ping ynov.com
ynov.com resolved to 104.26.10.233

84 bytes from 104.26.10.233 icmp_seq=1 ttl=59 time=30.735 ms
84 bytes from 104.26.10.233 icmp_seq=2 ttl=59 time=30.994 ms
84 bytes from 104.26.10.233 icmp_seq=3 ttl=59 time=31.433 ms
84 bytes from 104.26.10.233 icmp_seq=4 ttl=59 time=30.752 ms
84 bytes from 104.26.10.233 icmp_seq=5 ttl=59 time=30.986 ms
```

## 3. Bonus

### A. ACL

**🌞 Le réseau 10.7.30.0/24...**

```txt
conf t
access-list 30 permit 10.7.30.67
access-list 30 deny 10.7.30.0 0.0.0.255
access-list 30 permit any  
interface fastEthernet1/0
ip access-group 30 out            
exit
interface fastEthernet1/0.10
ip access-group 30 out            
exit
interface fastEthernet1/0.20
ip access-group 30 out            
exit
interface fastEthernet1/0.30
ip access-group 30 out            
exit
exit

```

### B. Spanning-tree

**🌞 Configuration de...**

- BPDUGuard
- PortFast

```shell
# Similaire sur les autres switchs
IOU7#sh spanning-tree summary                
Switch is in pvst mode
Root bridge for: none
Extended system ID                      is enabled
Portfast Default                        is edge
Portfast Edge BPDU Guard Default        is enabled
```

### C. Observe then destroy then observe

**🌞 Vérifier, à l'aide de commandes dédiées**

```shell
R1#sh standby br
                     P indicates configured to preempt.
                     |
Interface   Grp Prio P State    Active          Standby         Virtual IP     
Fa1/0.10    10  150  P Active   local           10.7.10.253     10.7.10.254    
Fa1/0.20    20  150  P Active   local           10.7.20.253     10.7.20.254    
Fa1/0.30    30  100    Standby  10.7.30.253     local           10.7.30.254  

IOU1#sh etherchannel summary 
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

        M - not in use, minimum links not met
        m - not in use, port not aggregated due to minimum links not met
        u - unsuitable for bundling
        w - waiting to be aggregated
        d - default port

        A - formed by Auto LAG


Number of channel-groups in use: 1
Number of aggregators:           1

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)          -        Et0/1(P)    Et0/2(P)    
```

**🌞 Couper le routeur prioritaire**

```shell
84 bytes from 1.1.1.1 icmp_seq=37 ttl=59 time=131.810 ms
84 bytes from 1.1.1.1 icmp_seq=38 ttl=59 time=58.984 ms
84 bytes from 1.1.1.1 icmp_seq=39 ttl=59 time=129.648 ms
1.1.1.1 icmp_seq=40 timeout
1.1.1.1 icmp_seq=41 timeout
1.1.1.1 icmp_seq=42 timeout
1.1.1.1 icmp_seq=43 timeout
84 bytes from 1.1.1.1 icmp_seq=44 ttl=59 time=114.136 ms
84 bytes from 1.1.1.1 icmp_seq=45 ttl=59 time=116.249 ms
84 bytes from 1.1.1.1 icmp_seq=46 ttl=59 time=173.280 ms
```

**🌞 Couper un switch crucial dans la topo STP**

![CA MARCHEEEEEE](/IMG/image.png)