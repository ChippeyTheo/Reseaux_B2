```shell
R5#show running-config 
Building configuration...

Current configuration : 1069 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R5
!
boot-start-marker
boot-end-marker
!
!
no aaa new-model
no ip icmp rate-limit unreachable
!
!
ip cef
no ip domain lookup
!       
!         
ip tcp synwait-time 5
!                 
!         
interface FastEthernet0/0
 ip address 10.6.25.1 255.255.255.252
 duplex half
!         
interface FastEthernet1/0
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
interface FastEthernet1/1
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
interface FastEthernet2/0
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
interface FastEthernet2/1
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
!         
ip forward-protocol nd
!         
no ip http server
no ip http secure-server
!         
!         
no cdp log mismatch duplex
!                 
!         
control-plane
!                
!         
gatekeeper
 shutdown 
!         
!         
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
 stopbits 1
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
 stopbits 1
line vty 0 4
 login    
!         
!         
end  
```