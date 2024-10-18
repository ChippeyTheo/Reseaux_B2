```shell
R1#show running-config 
Building configuration...

Current configuration : 1482 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
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
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex half
!         
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.1.10.254 255.255.255.0
!         
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.1.20.254 255.255.255.0
!         
interface FastEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.1.30.254 255.255.255.0
!         
interface FastEthernet1/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
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
ip nat inside source list 1 interface FastEthernet1/0 overload
!         
access-list 1 permit any
no cdp log mismatch duplex
!         
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