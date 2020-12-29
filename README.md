# Jarkom_Modul5_Lapres_T18

#### Subnetting (Pembagian IP) <br>
- Menentukan subnet yang ada dalam topologi dan lakukan labelling netmask terhadap masing-masing subnet kemudian menggabungkan subnet-subnet sampai menjadi subnet besar. <br>
![SubnetTopologi Modul 5](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/top.PNG)
- Pembagian IP dengan pohon berdasarkan penggabungan subnet yang telah dilakukan.
![TreeCIDR Modul5](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/tree.PNG) <br>
- Dari pohon tersebut akan mendapat pembagian IP sebagai berikut. <br>
![Pembagian IP](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/tabel.PNG) <br>

### Topologi
![Topologi](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/topologi.PNG) <br>
### Route
![Route](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/route.PNG) <br>
### No 1
mengkonfigurasi SURABAYA menggunakan iptables, tanpa menggunakan MASQUERADE
membuat ```satu.sh``` yang berisi </br>
``` iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.70.61``` </br>
![image](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/satu.PNG)

### No 2
mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER)  ```dua.sh``` yang berisi </br>
``` iptables -A FORWARD -p tcp --dport 22 -d 10.151.71.120/29 -i eth0 -j DROP``` </br>
![image](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/dua.PNG)
