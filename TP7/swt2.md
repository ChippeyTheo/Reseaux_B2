```shell
IOU2#sh running-config 
Building configuration...

Current configuration : 1805 bytes
exit
exit Last configuration change at 12:07:52 UTC Fri Nov 22 2024
exit
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
exit
hostname IOU2      
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