```

(sales router)

conf t
interface GigabitEthernet0/1
 description WAN_to_R-DEV
 ip address 192.0.2.1 255.255.255.252
 no shutdown
end
wr

conf t
router ospf 1
 router-id 1.1.1.1
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 192.0.2.0 0.0.0.3 area 0
 network 10.1.0.0 0.0.255.255 area 0
end
wr


(dev router)

conf t
interface GigabitEthernet0/1
 description WAN_to_R-SALES
 ip address 192.0.2.2 255.255.255.252
 no shutdown
end
wr

conf t
router ospf 1
 router-id 2.2.2.2
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 192.0.2.0 0.0.0.3 area 0
 network 10.2.0.0 0.0.255.255 area 0
end
wr

```


























```
