- un petit ```show running-config``` :

```shell
R3#sh running-config 
Building configuration...

Current configuration : 1208 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R3
!      
!         
interface FastEthernet0/0
 ip address 10.6.13.2 255.255.255.252
 duplex half
!         
interface FastEthernet1/0
 ip address 10.6.23.1 255.255.255.252
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
router ospf 3
 router-id 3.3.3.3
 log-adjacency-changes
 network 10.6.13.0 0.0.0.3 area 0
 network 10.6.23.0 0.0.0.3 area 0
!               
!         
end  
```

- ```show ip ospf neighbor``` + ```show ip route```:

```shell
R3#sh ip ospf neighbor 

Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/DR         00:00:39    10.6.23.2       FastEthernet1/0
1.1.1.1           1   FULL/DR         00:00:30    10.6.13.1       FastEthernet0/0
R3#sh ip route

Gateway of last resort is 10.6.23.2 to network 0.0.0.0

     10.0.0.0/8 is variably subnetted, 8 subnets, 2 masks
O       10.6.12.0/30 [110/2] via 10.6.23.2, 00:34:44, FastEthernet1/0
                     [110/2] via 10.6.13.1, 00:34:44, FastEthernet0/0
C       10.6.13.0/30 is directly connected, FastEthernet0/0
O IA    10.6.14.0/30 [110/2] via 10.6.13.1, 00:34:44, FastEthernet0/0
O IA    10.6.1.0/24 [110/3] via 10.6.13.1, 00:30:52, FastEthernet0/0
O IA    10.6.2.0/24 [110/3] via 10.6.13.1, 00:30:30, FastEthernet0/0
O IA    10.6.3.0/24 [110/2] via 10.6.13.1, 00:34:44, FastEthernet0/0
O IA    10.6.25.0/30 [110/2] via 10.6.23.2, 00:34:44, FastEthernet1/0
C       10.6.23.0/30 is directly connected, FastEthernet1/0
O*E2 0.0.0.0/0 [110/1] via 10.6.23.2, 00:27:52, FastEthernet1/0
```