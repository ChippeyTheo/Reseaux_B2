```shell
IOU6#sh running-config 
Building configuration...

Current configuration : 1477 bytes
exit
exit Last configuration change at 09:39:37 UTC Fri Nov 22 2024
exit
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
exit
hostname IOU6         
exit         
interface Ethernet0/0
exit         
interface Ethernet0/1
exit         
interface Ethernet0/2
 switchport access vlan 20
 switchport mode access
exit
```