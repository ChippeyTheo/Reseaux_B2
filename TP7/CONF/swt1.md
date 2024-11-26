```shell
IOU1#sh running-config 
Building configuration...     
exit         
spanning-tree mode pvst
spanning-tree extend system-id
exit               
exit         
interface Port-channel1
 switchport trunk allowed vlan 10,20,30
exit         
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit         
interface Ethernet0/1
 switchport trunk allowed vlan 10,20,30
 channel-group 1 mode on
exit         
interface Ethernet0/2
 switchport trunk allowed vlan 10,20,30
 channel-group 1 mode on
exit         
interface Ethernet0/3
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit         
interface Ethernet1/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit     
```