# 🔐 VLAN ACL Matrix

| VLAN | Description          | ACL Name         | SVI Direction | Allowed Internal (VLANs)        | Internet | Default for other internal | Notes |
|-----:|----------------------|------------------|---------------|----------------------------------|:-------:|:--------------------------:|-------|
| 10   | Support–Sales        | —                | —             | —                                |  Yes    | —                          | Open to all (no ACL). |
| 20   | Accounting           | ACL_VLAN20_IN    | IN            | 10, 30, 40                       |  Yes    | Deny                       | Deny to all other VLANs. |
| 30   | Accounts Manager     | ACL_VLAN30_IN    | IN            | 10, 20, 50, 120                  |  Yes    | Deny                       | — |
| 40   | Sales                | ACL_VLAN40_IN    | IN            | 60, 10, 50, 20, 30               |  Yes    | Deny                       | — |
| 50   | Sales Manager        | ACL_VLAN50_IN    | IN            | 60, 40, 10, 30, 120              |  Yes    | Deny                       | — |
| 60   | Reception            | ACL_VLAN60_IN    | IN            | 10, 40                           |  Yes    | Deny                       | — |
| 70   | Guests               | ACL_VLAN70_OUT*  | OUT (existing)| — (internal blocked)             |  Yes    | —                          | *Existing OUT ACL blocks internal; Internet only. |
| 110  | Support–Dev          | —                | —             | —                                |  Yes    | —                          | Open (no ACL). |
| 120  | Managers–Dev         | —                | —             | —                                |  Yes    | —                          | Open (no ACL). |
| 130  | Ops                  | ACL_VLAN130_IN   | IN            | 110, 120, 140                    |  Yes    | Deny                       | — |
| 140  | Dev                  | ACL_VLAN140_IN   | IN            | 110, 120, 130                    |  Yes    | Deny                       | — |
| 150  | Staff Wi-Fi          | ACL_VLAN150_IN   | IN            | 140, 130, 110, 120               |  Yes    | Deny                       | — |


```
(sales router)
(vlan 20)
conf t
ip access-list extended SALES-ACC-IN
 permit ip 10.1.20.0 0.0.0.255 10.1.10.0 0.0.0.255
 permit ip 10.1.20.0 0.0.0.255 10.1.30.0 0.0.0.255
 permit ip 10.1.20.0 0.0.0.255 10.1.40.0 0.0.0.255
 deny   ip 10.1.20.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.20.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.20
 ip access-group SALES-ACC-IN in
exit
end
wr

(vlan 30)
conf t
ip access-list extended SALES-ACC-MGR-IN
 permit ip 10.1.30.0 0.0.0.255 10.1.10.0 0.0.0.255
 permit ip 10.1.30.0 0.0.0.255 10.1.20.0 0.0.0.255
 permit ip 10.1.30.0 0.0.0.255 10.1.50.0 0.0.0.255
 permit ip 10.1.30.0 0.0.0.255 10.2.120.0 0.0.0.255
 deny   ip 10.1.30.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.30.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.30
 ip access-group SALES-ACC-MGR-IN in
exit
end
wr

(vlan 40)
conf t
ip access-list extended SALES-SALES-IN
 permit ip 10.1.40.0 0.0.0.255 10.1.60.0 0.0.0.255
 permit ip 10.1.40.0 0.0.0.255 10.1.10.0 0.0.0.255
 permit ip 10.1.40.0 0.0.0.255 10.1.50.0 0.0.0.255
 permit ip 10.1.40.0 0.0.0.255 10.1.20.0 0.0.0.255
 deny   ip 10.1.40.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.40.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.40
 ip access-group SALES-SALES-IN in
exit
end
wr


(vlan 50)
conf t
ip access-list extended SALES-MGR-IN
 permit ip 10.1.50.0 0.0.0.255 10.1.60.0 0.0.0.255
 permit ip 10.1.50.0 0.0.0.255 10.1.40.0 0.0.0.255
 permit ip 10.1.50.0 0.0.0.255 10.1.10.0 0.0.0.255
 permit ip 10.1.50.0 0.0.0.255 10.1.30.0 0.0.0.255
 permit ip 10.1.50.0 0.0.0.255 10.2.120.0 0.0.0.255
 deny   ip 10.1.50.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.50.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.50
 ip access-group SALES-MGR-IN in
exit
end
wr

(vlan 60)
conf t
ip access-list extended SALES-REC-IN
 permit ip 10.1.60.0 0.0.0.255 10.1.10.0 0.0.0.255
 permit ip 10.1.60.0 0.0.0.255 10.1.40.0 0.0.0.255
 deny   ip 10.1.60.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.60.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.60
 ip access-group SALES-REC-IN in
exit
end
wr

(vlan 70)
conf t
ip access-list extended GUEST-OUT
 deny   ip 10.1.70.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.1.70.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.70
 ip access-group GUEST-OUT out
exit
end
wr

(dev router)
(vlan 130)
conf t
ip access-list extended DEV-OPS-IN
 permit ip 10.2.130.0 0.0.0.255 10.2.110.0 0.0.0.255
 permit ip 10.2.130.0 0.0.0.255 10.2.120.0 0.0.0.255
 permit ip 10.2.130.0 0.0.0.255 10.2.140.0 0.0.0.255
 deny   ip 10.2.130.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.2.130.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.130
 ip access-group DEV-OPS-IN in
exit
end
wr

(vlan 140)
conf t
ip access-list extended DEV-DEV-IN
 permit ip 10.2.140.0 0.0.0.255 10.2.110.0 0.0.0.255
 permit ip 10.2.140.0 0.0.0.255 10.2.120.0 0.0.0.255
 permit ip 10.2.140.0 0.0.0.255 10.2.130.0 0.0.0.255
 deny   ip 10.2.140.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.2.140.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.140
 ip access-group DEV-DEV-IN in
exit
end
wr

(vlan 150)
conf t
ip access-list extended DEV-STAFFWIFI-IN
 permit ip 10.2.150.0 0.0.0.255 10.2.140.0 0.0.0.255
 permit ip 10.2.150.0 0.0.0.255 10.2.130.0 0.0.0.255
 permit ip 10.2.150.0 0.0.0.255 10.2.110.0 0.0.0.255
 permit ip 10.2.150.0 0.0.0.255 10.2.120.0 0.0.0.255
 deny   ip 10.2.150.0 0.0.0.255 10.0.0.0 0.255.255.255
 permit ip 10.2.150.0 0.0.0.255 any
exit
interface GigabitEthernet0/0.150
 ip access-group DEV-STAFFWIFI-IN in
exit
end
wr

```



