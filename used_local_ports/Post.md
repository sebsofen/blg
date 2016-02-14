mit NMAP kann man natürlich einfach die offenen Ports aller Geräte im Netzwerk finden.
Was aber, wenn auf der eigenen Maschine ein Port von einem laufenden Programm belegt ist?

Liste alle offenen Ports: ```sudo netstat -tulpn```. 

```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:139             0.0.0.0:*               LISTEN      844/smbd        
tcp        0      0 127.0.0.1:63342         0.0.0.0:*               LISTEN      20545/java      
tcp        0      0 127.0.0.1:54066         0.0.0.0:*               LISTEN      2506/java       
tcp        0      0 127.0.0.1:4371          0.0.0.0:*               LISTEN      17176/spotify   
tcp        0      0 0.0.0.0:57621           0.0.0.0:*               LISTEN      17176/spotify   
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      3460/dnsmasq    
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      16117/cupsd     
tcp        0      0 127.0.0.1:7000          0.0.0.0:*               LISTEN      2506/java       
tcp        0      0 127.0.0.1:4381          0.0.0.0:*               LISTEN      17176/spotify   
tcp        0      0 0.0.0.0:445             0.0.0.0:*               LISTEN      844/smbd        
tcp        0      0 127.0.0.1:6942          0.0.0.0:*               LISTEN      20545/java      
tcp        0      0 127.0.0.1:7199          0.0.0.0:*               LISTEN      2506/java       
tcp        0      0 0.0.0.0:37345           0.0.0.0:*               LISTEN      14651/skype     
tcp        0      0 127.0.0.1:8099          0.0.0.0:*               LISTEN      17176/spotify   
tcp        0      0 127.0.0.1:27017         0.0.0.0:*               LISTEN      1290/mongod     
tcp        0      0 0.0.0.0:54666           0.0.0.0:*               LISTEN      20545/java      
tcp6       0      0 :::139                  :::*                    LISTEN      844/smbd        
tcp6       0      0 :::8080                 :::*                    LISTEN      1775/java       
tcp6       0      0 :::8081                 :::*                    LISTEN      8038/main       
tcp6       0      0 :::57521                :::*                    LISTEN      2678/java       
tcp6       0      0 127.0.0.1:9042          :::*                    LISTEN      2506/java       
tcp6       0      0 ::1:631                 :::*                    LISTEN      16117/cupsd     
tcp6       0      0 127.0.0.1:8888          :::*                    LISTEN      19226/java      
tcp6       0      0 :::28667                :::*                    LISTEN      19226/java      
tcp6       0      0 :::32861                :::*                    LISTEN      20602/java      
tcp6       0      0 :::445                  :::*                    LISTEN      844/smbd        
tcp6       0      0 :::33152                :::*                    LISTEN      20602/java      
tcp6       0      0 127.0.0.1:8005          :::*                    LISTEN      1775/java       
udp        0      0 0.0.0.0:37345           0.0.0.0:*                           14651/skype     
udp        0      0 0.0.0.0:5353            0.0.0.0:*                           3296/chrome     
udp        0      0 0.0.0.0:5353            0.0.0.0:*                           696/avahi-daemon: r
udp        0      0 127.0.0.1:38736         0.0.0.0:*                           14651/skype     
udp        0      0 0.0.0.0:15760           0.0.0.0:*                           2675/dhclient   
udp        0      0 0.0.0.0:40739           0.0.0.0:*                           696/avahi-daemon: r
udp        0      0 127.0.1.1:53            0.0.0.0:*                           3460/dnsmasq    
udp        0      0 0.0.0.0:68              0.0.0.0:*                           2675/dhclient   
udp        0      0 192.168.113.255:137     0.0.0.0:*                           3589/nmbd       
udp        0      0 192.168.113.91:137      0.0.0.0:*                           3589/nmbd       
udp        0      0 0.0.0.0:137             0.0.0.0:*                           3589/nmbd       
udp        0      0 192.168.113.255:138     0.0.0.0:*                           3589/nmbd       
udp        0      0 192.168.113.91:138      0.0.0.0:*                           3589/nmbd       
udp        0      0 0.0.0.0:138             0.0.0.0:*                           3589/nmbd       
udp        0      0 0.0.0.0:57621           0.0.0.0:*                           17176/spotify   
udp        0      0 0.0.0.0:631             0.0.0.0:*                           1421/cups-browsed
udp6       0      0 :::5353                 :::*                                696/avahi-daemon: r
udp6       0      0 :::6736                 :::*                                2675/dhclient   
udp6       0      0 :::40456                :::*                                696/avahi-daemon: r
```

Was sehen wir? 

```
tcp6       0      0 127.0.0.1:9042          :::*                    LISTEN      2506/java 
```

Cassandra (9042) läuft schon! PID: 2506...
