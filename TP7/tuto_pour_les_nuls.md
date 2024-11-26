# Tuto pour faire le TP7 sans réfléchir de trop.

![intro](/IMG/coucou.png)

## Etape 1 : Faire la topologie sur GNS3.

**⚠️ Bien mettre les mêmes branchements que moi si vous ne voulez pas comprendre et copier bêtements l'étape 2**  

![shéma de la topologie](/IMG/image_tp7.png)

## Etape 2 : Copier/Coller les confs.

- **PC1**

```txt
ip 10.7.10.11/24 10.7.10.254
ip dns 1.1.1.1
```

- **PC2**

```txt
ip 10.7.20.11/24 10.7.20.254
```

- **PC3**

```txt
ip 10.7.20.12/24 10.7.20.254
```

- **PC4**

```txt
ip 10.7.30.67/24 10.7.30.254
```

- **PC5**

```txt
ip 10.7.30.11/24 10.7.30.254
```

- **switch 1**

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface range Ethernet 0/1 - 2
channel-group 1 mode on 
channel-protocol lacp
exit
interface port-channel 1
switchport trunk encapsulation dot1q
switchport mode trunk 
switchport trunk allowed vlan add 10,20,30
no shutdown
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit

```

- **switch 2**  
*ℹ️ le switch 1 et 2 possède la même conf*
![c'est pareil](/IMG/same-same.png)

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface range Ethernet 0/1 - 2
channel-group 1 mode on 
channel-protocol lacp
exit
interface port-channel 1
switchport trunk encapsulation dot1q
switchport mode trunk 
switchport trunk allowed vlan add 10,20,30
no shutdown
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit

```

- **switch 3**

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit
sh vlan br

show interface trunk


```

- **switch 4**  
*ℹ️ le switch 3 et 4 possède la même conf*
![c'est pareil](/IMG/same-same.png)

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit
sh vlan br

show interface trunk


```

- **switch 5**

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface Ethernet0/2
switchport mode access
switchport access vlan 10
exit
interface Ethernet0/3
switchport mode access
switchport access vlan 20
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit
sh vlan br

show interface trunk


```

- **switch 6**

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface Ethernet0/2
switchport mode access
switchport access vlan 20
exit
interface Ethernet0/3
switchport mode access
switchport access vlan 30
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit
sh vlan br

show interface trunk


```

- **switch 7**

```txt
conf t
vlan 10
name clients
exit
vlan 20
name admins
exit
vlan 30
name servers
exit
interface Ethernet0/2
switchport mode access
switchport access vlan 30
exit
interface Ethernet0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
interface Ethernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan add 10,20,30
exit
exit
sh vlan br

show interface trunk


```

- **routeur 1**

```txt
conf t
interface fastEthernet 0/0
ip nat outside
no shut
exit
interface fastEthernet 1/0
ip nat inside
no shut
exit
interface fastEthernet 1/0.10
encapsulation dot1q 10
ip address 10.7.10.252 255.255.255.0
ip nat inside
no shut
standby 10 ip 10.7.10.254
standby 10 priority 150
standby 10 preempt
exit
interface fastEthernet 1/0.20
encapsulation dot1q 20
ip address 10.7.20.252 255.255.255.0
ip nat inside
no shut
standby 20 ip 10.7.20.254
standby 20 priority 150
standby 20 preempt
exit
interface fastEthernet 1/0.30
encapsulation dot1q 30
ip address 10.7.30.252 255.255.255.0
ip nat inside
no shutdown
standby 30 ip 10.7.30.254
standby 30 priority 100
exit
access-list 1 permit any
ip nat inside source list 1 interface fastEthernet 0/0 overload
ip dns server
ip domain-lookup
ip name-server 1.1.1.1
interface fastEthernet 0/0
ip address dhcp
no shut
exit
exit

```

- **routeur 2**

```txt
conf t
interface fastEthernet 0/0
ip nat outside
no shut
exit
interface fastEthernet 1/0
ip nat inside
no shut
exit
interface fastEthernet 1/0.10
encapsulation dot1q 10
ip address 10.7.10.253 255.255.255.0
ip nat inside
no shut
standby 10 ip 10.7.10.254
standby 10 priority 100
exit
interface fastEthernet 1/0.20
encapsulation dot1q 20
ip address 10.7.20.253 255.255.255.0
ip nat inside
no shut
standby 20 ip 10.7.20.254
standby 20 priority 100
exit
interface fastEthernet 1/0.30
encapsulation dot1q 30
ip address 10.7.30.253 255.255.255.0
ip nat inside
no shutdown
standby 30 ip 10.7.30.254
standby 30 priority 150
standby 30 preempt
exit
access-list 1 permit any
ip nat inside source list 1 interface fastEthernet 0/0 overload
ip dns server
ip domain-lookup
ip name-server 1.1.1.1
interface fastEthernet 0/0
ip address dhcp
no shut
exit
exit

```

## Etape 3 : Prier pour que ca marche sinon j'ai fait une erreur. + les bonus.

### ACL pour le réseaux .30.

- **Sur les deux routeurs**

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

### B. Spanning-tree:

- **Sur tous les switchs**

```txt
conf t
spanning-tree portfast bpduguard default
spanning-tree portfast default
exit

```

