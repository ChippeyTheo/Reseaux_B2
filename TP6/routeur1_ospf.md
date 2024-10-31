- un petit ```show running-config``` :

```shell
R1#sh running-config 
Building configuration...

Current configuration : 1302 bytes
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
interface FastEthernet0/0
 ip address 10.6.13.1 255.255.255.252
 duplex half
!         
interface FastEthernet1/0
 ip address 10.6.12.1 255.255.255.252
 duplex auto
 speed auto
!         
interface FastEthernet1/1
 ip address 10.6.14.1 255.255.255.252
 duplex auto
 speed auto
!         
interface FastEthernet2/0
 ip address 10.6.3.254 255.255.255.0
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
router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes
 network 10.6.3.0 0.0.0.255 area 3
 network 10.6.12.0 0.0.0.3 area 0
 network 10.6.13.0 0.0.0.3 area 0
 network 10.6.14.0 0.0.0.3 area 3
!              
!         
gatekeeper
 shutdown 
!         
!                
end  
```

- ```show ip ospf neighbor``` + ```show ip route```:

```shell
R1#sh ip ospf neighbor 

Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/BDR        00:00:34    10.6.12.2       FastEthernet1/0
3.3.3.3           1   FULL/BDR        00:00:32    10.6.13.2       FastEthernet0/0
4.4.4.4           1   FULL/BDR        00:00:38    10.6.14.2       FastEthernet1/1

R1#show ip route

Gateway of last resort is 10.6.12.2 to network 0.0.0.0

     10.0.0.0/8 is variably subnetted, 8 subnets, 2 masks
C       10.6.12.0/30 is directly connected, FastEthernet1/0
C       10.6.13.0/30 is directly connected, FastEthernet0/0
C       10.6.14.0/30 is directly connected, FastEthernet1/1
O       10.6.1.0/24 [110/2] via 10.6.14.2, 00:10:48, FastEthernet1/1
O       10.6.2.0/24 [110/2] via 10.6.14.2, 00:10:48, FastEthernet1/1
C       10.6.3.0/24 is directly connected, FastEthernet2/0
O IA    10.6.25.0/30 [110/2] via 10.6.12.2, 00:10:48, FastEthernet1/0
O       10.6.23.0/30 [110/2] via 10.6.13.2, 00:15:02, FastEthernet0/0
                     [110/2] via 10.6.12.2, 00:15:02, FastEthernet1/0
O*E2 0.0.0.0/0 [110/1] via 10.6.12.2, 00:08:09, FastEthernet1/0
```

