```shell
IOU5#sh running-config 
Building configuration...

Current configuration : 1528 bytes
exit
exit Last configuration change at 09:39:38 UTC Fri Nov 22 2024
exit
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
exit
hostname IOU5       
exit         
interface Ethernet0/0
exit         
interface Ethernet0/1
exit         
interface Ethernet0/2
 switchport access vlan 10
 switchport mode access
exit         
interface Ethernet0/3
 switchport access vlan 20
 switchport mode access
exit 
```