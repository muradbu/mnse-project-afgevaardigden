
`agg-noord` packet tracer we created:

```
agg-noord#show running-config 
Building configuration...

Current configuration : 1227 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname agg-noord
!
!
!
!
!
!
!
!
ip cef
no ipv6 cef
!
!
!
!
license udi pid CISCO2911/K9 sn FTX152498L6-
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0
 ip address 10.255.0.49 255.255.255.252
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 ip address 10.0.0.10 255.255.255.252
!
interface GigabitEthernet0/1.20
 encapsulation dot1Q 20
 ip address 10.0.0.14 255.255.255.252
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes
 redistribute bgp 65503 subnets 
 network 10.0.0.8 0.0.0.3 area 0
 network 10.0.0.12 0.0.0.3 area 0
!
router bgp 65503
 bgp router-id 1.1.1.1
 bgp log-neighbor-changes
 no synchronization
 neighbor 10.255.0.50 remote-as 65501
 network 10.255.0.48 mask 255.255.255.252
 redistribute ospf 1 
!
ip classless
!
ip flow-export version 9
!
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end
```
