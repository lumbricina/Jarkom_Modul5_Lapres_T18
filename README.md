# Jarkom_Modul5_Lapres_T18

### No 1
mengkonfigurasi SURABAYA menggunakan iptables, tanpa menggunakan MASQUERADE
membuat ```satu.sh``` yang berisi
``` iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.70.61```

### No 2
mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER)  ```dua.sh``` yang berisi
``` iptables -A FORWARD -p tcp --dport 22 -d 10.151.71.120/29 -i eth0 -j DROP```
