```

(sales location)

(main sw)
conf t
interface fa0/2
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr

(acc sw)
conf t
interface range fa0/4-22
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr

(managment sw)
conf t
interface range fa0/2-3
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr

(reception & client sw)
conf t
interface range fa0/2-7
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr



(dev location)

(dev sw)
conf t
interface range fa0/3-22
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr

(ops sw)
conf t
interface range fa0/2-22
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr

(managments & support)
conf t
interface range fa0/2-10
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
end
wr






```
