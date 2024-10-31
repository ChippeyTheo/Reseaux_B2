- un petit ```show running-config``` :

```shell
R4#sh running-config 
Building configuration...

Current configuration : 1255 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R4
!      
!         
interface FastEthernet0/0
 ip address 10.6.14.2 255.255.255.252
 duplex half
!         
interface FastEthernet1/0
 ip address 10.6.1.254 255.255.255.0
 duplex auto
 speed auto
!         
interface FastEthernet1/1
 ip address 10.6.2.254 255.255.255.0
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
router ospf 4
 router-id 4.4.4.4
 log-adjacency-changes
 network 10.6.1.0 0.0.0.255 area 3
 network 10.6.2.0 0.0.0.255 area 3
 network 10.6.14.0 0.0.0.3 area 3
!                 
!         
end 
```

- ```show ip ospf neighbor``` + ```show ip route```:

```shell
R4#sh ip ospf neighbor 

Neighbor ID     Pri   State           Dead Time   Address         Interface
1.1.1.1           1   FULL/DR         00:00:35    10.6.14.1       FastEthernet0/0
R4#sh ip route

Gateway of last resort is 10.6.14.1 to network 0.0.0.0

     10.0.0.0/8 is variably subnetted, 8 subnets, 2 masks
O IA    10.6.12.0/30 [110/2] via 10.6.14.1, 00:33:24, FastEthernet0/0
O IA    10.6.13.0/30 [110/2] via 10.6.14.1, 00:33:24, FastEthernet0/0
C       10.6.14.0/30 is directly connected, FastEthernet0/0
C       10.6.1.0/24 is directly connected, FastEthernet1/0
C       10.6.2.0/24 is directly connected, FastEthernet1/1
O       10.6.3.0/24 [110/2] via 10.6.14.1, 00:33:24, FastEthernet0/0
O IA    10.6.25.0/30 [110/3] via 10.6.14.1, 00:33:24, FastEthernet0/0
O IA    10.6.23.0/30 [110/3] via 10.6.14.1, 00:33:24, FastEthernet0/0
O*E2 0.0.0.0/0 [110/1] via 10.6.14.1, 00:30:46, FastEthernet0/0
```