```shell
IOU4#sh running-config 
Building configuration...

Current configuration : 1731 bytes
exit
exit Last configuration change at 09:39:38 UTC Fri Nov 22 2024
exit
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
exit
hostname IOU4        
exit         
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit         
interface Ethernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit         
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
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