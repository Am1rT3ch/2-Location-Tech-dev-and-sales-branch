```

(wifi router on dev location)

(main sw)
conf t
interface fa0/4
 description Staff_WiFi_AP
 switchport mode access
 switchport access vlan 150
 no shutdown
 no switchport port-security
end
wr

** Local IP Address: 10.2.150.2

** Subnet Mask: 255.255.255.0

** DHCP Server: Disable

(wifi router on sales location)

(main sw)
conf t
interface fa0/24
 description Staff_WiFi_AP
 switchport mode access
 switchport access vlan 70
 no shutdown
 no switchport port-security
end
wr

```
