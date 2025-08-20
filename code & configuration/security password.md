```
on every router & on every switch:
conf t
enable secret 1234
service password-encryption
line console 0
password 1234
login exec-timeout 10 0
logging synchronous
exit
end
wr
```
