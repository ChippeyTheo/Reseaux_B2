```shell
R1#sh running-config 
Building configuration...

Current configuration : 1784 bytes
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
ip name-server 1.1.1.1
!        
!         
ip tcp synwait-time 5
!                 
!         
interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex half
!         
interface FastEthernet1/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!         
interface FastEthernet1/0.10
 encapsulation dot1Q 10
 ip address 10.7.10.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 10 ip 10.7.10.254
 standby 10 priority 150
 standby 10 preempt
!         
interface FastEthernet1/0.20
 encapsulation dot1Q 20
 ip address 10.7.20.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 20 ip 10.7.20.254
 standby 20 priority 150
 standby 20 preempt
!         
interface FastEthernet1/0.30
 encapsulation dot1Q 30
 ip address 10.7.30.252 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 standby 30 ip 10.7.30.254
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
ip dns server
!         
ip nat inside source list 1 interface FastEthernet0/0 overload
!         
access-list 1 permit any
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