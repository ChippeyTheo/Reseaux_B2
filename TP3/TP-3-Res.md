# TP3 INFRA : Premiers pas GNS, Cisco et VLAN

## I. Dumb switch

### 3. Setup topologie 1

**🌞 Commençons simple**

- ```shell
    PC1> ping 10.3.1.2         

    84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=2.127 ms
    84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=1.591 ms
    ```

- ```shell
    IOU1#show mac address-table
              Mac Address Table
    -------------------------------------------

    Vlan    Mac Address       Type        Ports
    ----    -----------       --------    -----
       1    0050.7966.6800    DYNAMIC     Et0/0
       1    0050.7966.6801    DYNAMIC     Et0/1
    Total Mac Addresses for this criterion: 2
    ```

## II. VLAN

**🌞 Adressage**

```shell
PC3> ping 10.3.1.1
84 bytes from 10.3.1.1 icmp_seq=1 ttl=64 time=2.522 ms
^C
PC3> ping 10.3.1.2
84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=2.168 ms


PC1> ping 10.3.1.2
84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=1.129 ms
^C
PC1> ping 10.3.1.3
84 bytes from 10.3.1.3 icmp_seq=1 ttl=64 time=1.508 ms
```

**🌞 Configuration des VLANs**

```shell
IOU1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/0, Et0/1, Et0/2, Et0/3
                                                Et1/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                                Et3/0, Et3/1, Et3/2, Et3/3
10   admins                           active    
20   guests                           active    
1002 fddi-default                     act/unsup 
1003 token-ring-default               act/unsup 
1004 fddinet-default                  act/unsup 
1005 trnet-default                    act/unsup 

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0   
10   enet  100010     1500  -      -      -        -    -        0      0   
20   enet  100020     1500  -      -      -        -    -        0      0   
1002 fddi  101002     1500  -      -      -        -    -        0      0   
1003 tr    101003     1500  -      -      -        -    -        0      0   
1004 fdnet 101004     1500  -      -      -        ieee -        0      0   
1005 trnet 101005     1500  -      -      -        ibm  -        0      0   
 --More-- 
```

**🌞 Vérif**

```shell
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=1.303 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=1.144 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=1.362 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=1.411 ms
^C
PC1> ping 10.3.1.3
host (10.3.1.3) not reachable


PC3> ping 10.3.1.2

host (10.3.1.2) not reachable
```

## III. Ptite VM DHCP

- installez un serveur DHCP

```shell
default-lease-time 900;
max-lease-time 10800;

authoritative;

subnet 10.3.1.0 netmask 255.255.255.0 {
range 10.3.1.100 10.3.1.200;
option subnet-mask 255.255.255.0;
option domain-name-servers 10.3.1.1;
}
~        
```

- vérifier avec le pc4 que vous pouvez récupérer une IP en DHCP

```shell
PC4> ip dhcp
DORA
PC4> show ip IP 10.3.1.100/24

NAME        : PC4[1]
IP/MASK     : 10.3.1.100/24
GATEWAY     : 0.0.0.0
DNS         : 10.3.1.1  
DHCP SERVER : 10.3.1.254
DHCP LEASE  : 896, 900/450/787
MAC         : 00:50:79:66:68:03
LPORT       : 20017
RHOST:PORT  : 127.0.0.1:20018
MTU         : 1500
```

- vérifier avec le pc5 que vous ne pouvez PAS récupérer une IP en DHCP

```shell
PC5> ip dhcp
DDD
Can't find dhcp server
```