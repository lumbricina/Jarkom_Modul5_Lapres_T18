# Jarkom_Modul5_Lapres_T18

#### Subnetting (Pembagian IP) <br>
- Menentukan subnet yang ada dalam topologi dan lakukan labelling netmask terhadap masing-masing subnet kemudian menggabungkan subnet-subnet sampai menjadi subnet besar. <br>
![SubnetTopologi Modul 5](https://user-images.githubusercontent.com/61286109/102895716-c7eed280-4497-11eb-9344-008e4d53366b.png) <br>
Hasil yang didapat adalah <b>Netmask /21</b> untuk subnet besar topologi diatas.
- Pembagian IP dengan pohon berdasarkan penggabungan subnet yang telah dilakukan.
![TreeCIDR Modul5](https://user-images.githubusercontent.com/61286109/102901541-58311580-44a0-11eb-9e8e-62e186f6eda4.png) <br>
- Dari pohon tersebut akan mendapat pembagian IP sebagai berikut. <br>
![Pembagian IP](https://user-images.githubusercontent.com/61286109/102895979-3fbcfd00-4498-11eb-8706-a60ed977048d.PNG) <br>

#### Konfigurasi Tiap UML
1. Pertama, membuat file `topologi.sh`.
![NanoTopologi](https://user-images.githubusercontent.com/61286109/102784082-73cbeb80-43ce-11eb-89e5-5bfb656220a9.PNG) <br>
2. Pada semua UML Router, ke file `nano /etc/sysctl.conf` kemudian uncomment `net.ipv4.ip_forward=1` dan aktifkan dengan syntax `sysctl -p`. <br>
3. Lakukan setting interface pada semua UML di `nano /etc/network/interfaces` dan di restart dengan syntax `service networking restart`. <br>
- ROUTER SURABAYA <br>
![iface surabaya](https://user-images.githubusercontent.com/61286109/102900032-55352580-449e-11eb-8844-8224bb6b9db2.PNG) <br>
- ROUTER KEDIRI <br>
![iface kediri](https://user-images.githubusercontent.com/61286109/102899925-3767c080-449e-11eb-8854-e8714623d1c4.PNG) <br>
- ROUTER BATU <br>
![iface batu](https://user-images.githubusercontent.com/61286109/102899633-d0e2a280-449d-11eb-95ed-e3ea0a41ca32.PNG) <br>
- SERVER MADIUN <br>
![iface madiun](https://user-images.githubusercontent.com/61286109/102902989-4badbc80-44a2-11eb-972d-58845f439e48.PNG) <br>
- SERVER PROBOLINGGO <br>
![iface probolinggo](https://user-images.githubusercontent.com/61286109/102902985-494b6280-44a2-11eb-9da6-de197f677452.PNG) <br>
- SERVER MALANG <br>
![iface malang](https://user-images.githubusercontent.com/61286109/102900739-4ef37900-449f-11eb-9809-13a3a6b25ac0.PNG) <br>
- SERVER MOJOKERTO <br>
![iface mojokerto](https://user-images.githubusercontent.com/61286109/102900727-4bf88880-449f-11eb-8bfb-4095fa168432.PNG) <br>
- KLIEN GRESIK <br>
![iface gresik](https://user-images.githubusercontent.com/61286109/102826852-0cd12580-4414-11eb-8710-1234c41f2c70.PNG) <br>
- KLIEN SIDOARJO <br>
![iface sidoarjo](https://user-images.githubusercontent.com/61286109/102826859-0fcc1600-4414-11eb-9b38-f57858a26aa6.PNG) <br>
4. Lakukan Routing terhadap Router Surabaya dengan membuat file dengan `nano routing.sh` untuk memudahkan kita karena pada saat setiap UML di restart maka routenya ke reset. Untuk menjalankannya ketik syntax `source routing.sh`.
- ROUTING SURABAYA <br>
![routing surabaya](https://user-images.githubusercontent.com/61286109/102912675-47889b80-44b0-11eb-9f89-5b2f4a1d4440.PNG) <br>
- ROUTING KEDIRI <br>
![routing kediri](https://user-images.githubusercontent.com/61286109/102912665-45bed800-44b0-11eb-9509-163626b42c1c.PNG) <br>

5. Install DHCP server, DHCP Relay, DNS server dan Web server
Jalankan perintah `apt-get update` sebelum menginstall pada UML
- MALANG (DNS Server) <br>
Gunakan command `apt-get install bind9 -y` untuk menginstall Bind9 <br>
<img width="364" alt="dns server" src="https://user-images.githubusercontent.com/26424136/102977306-63825080-4535-11eb-9e09-a4fd4849cc57.PNG"> <br>
- MOJOKERTO (DHCP Server) <br>
Gunakan command `apt-get install isc-dhcp-server` untuk menginstall DHCP Server <br>
<img width="369" alt="dhcp server" src="https://user-images.githubusercontent.com/26424136/102977301-61b88d00-4535-11eb-903e-588d5cc6c906.PNG"> <br>
- SURABAYA, BATU dan KEDIRI (DHCP Relay) <br>
Gunakan command `apt-get install isc-dhcp-relay` untuk menginstall DHCP Relay <br>
DHCP RELAY SURABAYA <br>
![relay surabaya](https://user-images.githubusercontent.com/61286109/103164621-4d7bd500-4840-11eb-9530-7a40f61e0276.PNG) <br>
DHCP RELAY BATU <br>
![relay batu](https://user-images.githubusercontent.com/61286109/103164623-4f459880-4840-11eb-9ee7-aa9a48f1528c.PNG) <br>
DHCP RELAY KEDIRI <br>
![relay kediri](https://user-images.githubusercontent.com/61286109/103164624-4fde2f00-4840-11eb-8df5-9f99771015b8.PNG) <br>
- MADIUN dan PROBOLINGGO (Web Server) <br>
Gunakan command `apt-get install apache2` untuk menginstall Web Server Apache <br>
WEB SERVER PROBOLINGGO <br>
![web server probolinggo](https://user-images.githubusercontent.com/61286109/103164757-bc0d6280-4841-11eb-9a3d-82902ef82032.PNG) <br>
WEB SERVER MADIUN <br>
![web server madiun](https://user-images.githubusercontent.com/61286109/103164756-ba439f00-4841-11eb-836b-1eb0b62ecc04.PNG) <br>

### No 1
mengkonfigurasi SURABAYA menggunakan iptables, tanpa menggunakan MASQUERADE
membuat ```satu.sh``` yang berisi </br>
``` iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.70.61``` </br>
![image](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/satu.PNG)

### No 2
mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER)  ```dua.sh``` yang berisi </br>
``` iptables -A FORWARD -p tcp --dport 22 -d 10.151.71.120/29 -i eth0 -j DROP``` </br>
![image](https://github.com/lumbricina/Jarkom_Modul5_Lapres_T18/blob/main/Assets/dua.PNG)
