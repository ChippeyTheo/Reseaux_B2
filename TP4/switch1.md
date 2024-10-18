```shell
IOU2#show running-config 
Building configuration...

Current configuration : 1609 bytes
!
! Last configuration change at 12:58:34 UTC Fri Oct 18 2024
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname IOU2
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL 
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
!       
!         
no ip icmp rate-limit unreachable
!                  
!         
no ip domain-lookup
no ip cef 
no ipv6 cef
!               
!         
spanning-tree mode pvst
spanning-tree extend system-id
!                 
!         
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
!         
interface Ethernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
!         
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
!         
interface Ethernet0/3
!         
interface Ethernet1/0
!         
interface Ethernet1/1
!         
interface Ethernet1/2
!         
interface Ethernet1/3
!         
interface Ethernet2/0
!         
interface Ethernet2/1
!         
interface Ethernet2/2
!         
interface Ethernet2/3
!         
interface Ethernet3/0
!         
interface Ethernet3/1
!         
interface Ethernet3/2
!         
interface Ethernet3/3
!         
interface Vlan1
 no ip address
 shutdown 
!         
ip forward-protocol nd
!         
ip tcp synwait-time 5
ip http server
!         
ip ssh server algorithm encryption aes128-ctr aes192-ctr aes256-ctr
ip ssh client algorithm encryption aes128-ctr aes192-ctr aes256-ctr
!               
!         
control-plane
!         
!         
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 4
 login    
!         
!         
!         
end
```