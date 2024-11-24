# Tuto pour faire le TP7 sans réfléchir de trop.

## Etape 1 : Faire la topologie sur GNS3.

**⚠️ Bien mettre les mêmes branchements que moi si vous ne voulez pas comprendre et copier bêtements l'étape 2**  

![shéma de la topologie](/TP7/image_tp7.png)

## Etape 2 : Copier/Coller les confs.

- **PC1**

```txt
ip 10.7.10.11/24 10.7.10.254
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



## Etape 3 : Prier pour que ca marche sinon j'ai fait une erreur.