```

(on the sales router)

conf t
interface GigabitEthernet0/0
 no ip address
 no shutdown

interface GigabitEthernet0/0.10
 encapsulation dot1q 10
 ip address 10.1.10.1 255.255.255.0

interface GigabitEthernet0/0.20
 encapsulation dot1q 20
 ip address 10.1.20.1 255.255.255.0

interface GigabitEthernet0/0.30
 encapsulation dot1q 30
 ip address 10.1.30.1 255.255.255.0

interface GigabitEthernet0/0.40
 encapsulation dot1q 40
 ip address 10.1.40.1 255.255.255.0

interface GigabitEthernet0/0.50
 encapsulation dot1q 50
 ip address 10.1.50.1 255.255.255.0

interface GigabitEthernet0/0.60
 encapsulation dot1q 60
 ip address 10.1.60.1 255.255.255.0

interface GigabitEthernet0/0.70
 encapsulation dot1q 70
 ip address 10.1.70.1 255.255.255.0
exit

ip dhcp excluded-address 10.1.10.1 10.1.10.20
ip dhcp excluded-address 10.1.20.1 10.1.20.20
ip dhcp excluded-address 10.1.30.1 10.1.30.20
ip dhcp excluded-address 10.1.40.1 10.1.40.20
ip dhcp excluded-address 10.1.50.1 10.1.50.20
ip dhcp excluded-address 10.1.60.1 10.1.60.20
ip dhcp excluded-address 10.1.70.1 10.1.70.20

ip dhcp pool SALES-10
 network 10.1.10.0 255.255.255.0
 default-router 10.1.10.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-20
 network 10.1.20.0 255.255.255.0
 default-router 10.1.20.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-30
 network 10.1.30.0 255.255.255.0
 default-router 10.1.30.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-40
 network 10.1.40.0 255.255.255.0
 default-router 10.1.40.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-50
 network 10.1.50.0 255.255.255.0
 default-router 10.1.50.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-60
 network 10.1.60.0 255.255.255.0
 default-router 10.1.60.1
 dns-server 8.8.8.8 
exit
ip dhcp pool SALES-70
 network 10.1.70.0 255.255.255.0
 default-router 10.1.70.1
 dns-server 8.8.8.8 
exit
end
wr


(on the dev router)

conf t
interface GigabitEthernet0/0
 no ip address
 no shutdown

interface GigabitEthernet0/0.110
 encapsulation dot1q 110
 ip address 10.2.110.1 255.255.255.0

interface GigabitEthernet0/0.120
 encapsulation dot1q 120
 ip address 10.2.120.1 255.255.255.0

interface GigabitEthernet0/0.130
 encapsulation dot1q 130
 ip address 10.2.130.1 255.255.255.0

interface GigabitEthernet0/0.140
 encapsulation dot1q 140
 ip address 10.2.140.1 255.255.255.0

interface GigabitEthernet0/0.150
 encapsulation dot1q 150
 ip address 10.2.150.1 255.255.255.0
exit


ip dhcp excluded-address 10.2.110.1 10.2.110.20
ip dhcp excluded-address 10.2.120.1 10.2.120.20
ip dhcp excluded-address 10.2.130.1 10.2.130.20
ip dhcp excluded-address 10.2.140.1 10.2.140.20
ip dhcp excluded-address 10.2.150.1 10.2.150.20

ip dhcp pool DEV-110
 network 10.2.110.0 255.255.255.0
 default-router 10.2.110.1
 dns-server 8.8.8.8
exit
ip dhcp pool DEV-120
 network 10.2.120.0 255.255.255.0
 default-router 10.2.120.1
 dns-server 8.8.8.8 
exit
ip dhcp pool DEV-130
 network 10.2.130.0 255.255.255.0
 default-router 10.2.130.1
 dns-server 8.8.8.8 
exit
ip dhcp pool DEV-140
 network 10.2.140.0 255.255.255.0
 default-router 10.2.140.1
 dns-server 8.8.8.8 
exit
ip dhcp pool DEV-150
 network 10.2.150.0 255.255.255.0
 default-router 10.2.150.1
 dns-server 8.8.8.8
exit
end
wr


```




