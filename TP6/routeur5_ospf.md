- un petit ```show running-config``` :

```shell
R5#sh running-config 
Building configuration...

Current configuration : 1318 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R5
!        
!         
interface FastEthernet0/0
 ip address 10.6.25.1 255.255.255.252
 duplex half
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
router ospf 5
 router-id 5.5.5.5
 log-adjacency-changes
 network 10.6.25.0 0.0.0.3 area 1
 default-information originate always
!         
ip forward-protocol nd
!                 
ip nat inside source list 1 interface FastEthernet1/0 overload
!         
access-list 1 permit any
!                  
!         
end
```

- ```show ip ospf neighbor``` + ```show ip route```:

```shell
R5#sh ip ospf neighbor 

Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/DR         00:00:31    10.6.25.2       FastEthernet0/0
R5#sh ip route

Gateway of last resort is 192.168.122.1 to network 0.0.0.0

C    192.168.122.0/24 is directly connected, FastEthernet1/0
     10.0.0.0/8 is variably subnetted, 8 subnets, 2 masks
O IA    10.6.12.0/30 [110/2] via 10.6.25.2, 00:33:43, FastEthernet0/0
O IA    10.6.13.0/30 [110/3] via 10.6.25.2, 00:33:43, FastEthernet0/0
O IA    10.6.14.0/30 [110/3] via 10.6.25.2, 00:33:43, FastEthernet0/0
O IA    10.6.1.0/24 [110/4] via 10.6.25.2, 00:33:43, FastEthernet0/0
O IA    10.6.2.0/24 [110/4] via 10.6.25.2, 00:33:43, FastEthernet0/0
O IA    10.6.3.0/24 [110/3] via 10.6.25.2, 00:33:43, FastEthernet0/0
C       10.6.25.0/30 is directly connected, FastEthernet0/0
O IA    10.6.23.0/30 [110/2] via 10.6.25.2, 00:33:43, FastEthernet0/0
S*   0.0.0.0/0 [254/0] via 192.168.122.1
```