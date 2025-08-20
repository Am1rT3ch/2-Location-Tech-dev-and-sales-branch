```
**SALES LOCATION**
vlan config:
(on every switch in sales location)
enable 
conf t
vlan 10 
name SUPPORT
vlan 20 
name ACCOUNTING
vlan 30 
name ACC_MANAGER
vlan 40 
name SALES
vlan 50 
name SALES_MANAGER
vlan 60 
name RECEPTION
vlan 70 
name GUEST_WIFI
vlan 998 
name NATIVE
vlan 999 
name UNUSED
end
wr

(on main switch)
conf t
interface fastEthernet0/1
 description Uplink_to_R-SALES
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown
 
(for the access switch & wifi router)
 interface range FastEthernet0/23 - 24
 description Uplinks_to_Access_Switches
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown

(for tech support)
conf t
interface fa0/2
description Techsupport
switchport mode access
switchport access vlan 10
no shutdown
end
wr


(acc switch)
conf t
default interface range fa0/4 - 22
interface range fa0/4 - 22
description Accounting_PCs
switchport mode access
switchport access vlan 20
no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown
end
wr

interface range FastEthernet0/2 - 3
 description Uplinks_to_Access_Switches
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown
end
wr

(sales & reception sw)
conf t
interface range fa0/2 - 4
 description Sales_Desks
 switchport mode access
 switchport access vlan 40
 no shutdown

interface range fa0/5 - 7
 description Reception_Desks
 switchport mode access
 switchport access vlan 60
 no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown
end
wr


(for management sw)
conf t
interface fa0/2
 description Sales_Managers
 switchport mode access
 switchport access vlan 50
 no shutdown

interface fa0/3
 description Accountent_manager
 switchport mode access
 switchport access vlan 30
 no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 10,20,30,40,50,60,70
 no shutdown
end
wr

**DEV LOCATION**
vlan config:
(on every switch in dev location)

conf t
vlan 110
 name DEV_SUPPORT
vlan 120
 name MANAGERS
vlan 130
 name OPS
vlan 140
 name DEV
vlan 150
 name STAFF_WIFI
vlan 998
 name NATIVE
vlan 999
 name UNUSED
end
wr

(main dev sw)
conf t
interface fastEthernet0/1
 description Uplink_to_R-DEV
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown

interface range FastEthernet0/2 - 4
 description Uplinks_to_Access_Switches
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown
end
wr

(dev sw)
conf t
interface range fa0/3 - 22
 description Dev_Workstations
 switchport mode access
 switchport access vlan 140
 no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown
end
wr

interface FastEthernet0/2
 description Uplinks_to_Access_Switches
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown
end
wr

(ops sw)
conf t
interface range fa0/2 - 22
 description Ops_Workstations
 switchport mode access
 switchport access vlan 130
 no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown
end
wr

(managmet & techsupport sw)
conf t
interface range fa0/2 - 5
 description Managers
 switchport mode access
 switchport access vlan 120
 no shutdown

interface range fa0/6 - 10
 description Support
 switchport mode access
 switchport access vlan 110
 no shutdown

interface fa0/1
 description Up_to_Core
 switchport mode trunk
 switchport trunk native vlan 998
 switchport trunk allowed vlan 110,120,130,140,150
 no shutdown
end
wr
```
