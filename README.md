**Soal 1**

Membuat topologi sesuai soal, 2 switch dan 4 client
<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20164406.png" />

**Soal 2**

Menmbahkan NAT dan menyetting iptables di Router ERU 

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16
```

<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165315.png" />


**Soal 3**

Untuk memastikan bahwa setiap client dapat terhubung gunakan comand ping di ikuti ip tujuan

<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20162435.png" />

**Soal 4**

Agar setiap client bisah terhubung di internet yang bukan lokal tambahkan 

```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Untuk setiap client lalu lakukan uji coba dengn
```
ping google.com || apakah ada paket yang loss
```

<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20162515.png" />

**Soal 5**

Agar Konfigurasi yang sudah di lakukan tidak hilang kita bisa menyimpanyna di folder /root

<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165315.png" />
<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165448.png" />


**Soal 6**

langakah pertama download dan unzip file saya menggunkan script .sh untuk meakukannya secara otomatis
```
#!/bin/bash
wget --no-check-certificate "https://docs.google.com/uc?export=download&id=1bE3kF1Nclw0VyKq4bL2VtOOt53IC7lG5">unzip traffic.zip
chmod +x traffic.sh
./traffic.sh
```
<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20170232.png" >

sebelum melakukan run ```traffic.sh``` buka Gns3 dan klik kanan lalu lakukan start capture
untuk melakukan anlisa jaringan, jika sudah lakukan filter display 

```
ip.addr == 10.65.1.3
```

<img  width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20164956.png" >

**Soal 7**

Untuk Soal 7 membuat script ```.sh``` untuk melakukan install otomatis FTP server, membuat folder ```/shared```, config ftp server, membuat user ainur melkor dan membuat file uji coba untuk mengetes user

```
#!/bin/bash

pkill vsftpd

apt update -y
apt install -y ftp
apt install -y vsftpd

mkdir -p /shared
chmod 750 /shared
chmod 640 /shared/file_test.txt

cat > /etc/vsftpd.conf << 'EOF'
listen=YES
listen_ipv6=NO
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=NO
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
ssl_enable=NO
local_root=/shared
EOF

service vsftpd restart

useradd -m -s /bin/bash ainur 2>/dev/null
echo "ainur:123" | chpasswd

useradd -m -s /bin/bash melkor 2>/dev/null
echo "melkor:123" | chpasswd

chown ainur:ainur /shared
chmod 750 /shared

echo "Ambatukam,ambasing,ambatunat" > /shared/file_test.txt
chown ainur:ainur /shared/file_test.txt
```
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20213140.png" />
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20165754.png" />
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20165721.png" />

**Soal 8**

Untuk soal 8 membuat script ```.sh ```untuk melakukan download ,unzip file dan meabuat folder untuk tempat hasil unzipnya ini di node ```Ulmo```
```
#!/bin/bash

echo "=== DOWNLOAD FILE DARI GOOGLE DRIVE ==="

apt update && apt install -y wget unzip ftp file

GDRIVE_URL="https://drive.google.com/uc?export=download&id=11ra_yTV_adsPIXeIPMSt0vrxCBZu0r33"
OUTPUT_FILE="/root/ramalan_cuaca.zip"

echo "Mendownload file dari Google Drive..."
echo "URL: $GDRIVE_URL"
wget --no-check-certificate -O "$OUTPUT_FILE" "$GDRIVE_URL"

echo "Mengekstrak file ZIP..."
mkdir -p /root/extracted_files
unzip -o "$OUTPUT_FILE" -d /root/extracted_files/
```
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20170524.png" >

setelah menjalankan script nya buka gns3 client lalu klik kanan kaberl yang terhubung anatara eru dan ulmo untuk melakukan analisis file yang akan di upload
jika sudah ,masih di node ulmo instal ftp 
``` apt update && apt install -y ftp```
lalu masuk ke ftp user ainur menggunkan ip eru dan lakukan upload

<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20170642.png" >

Jika sudah masuk ke wireshark lagi lakukan filter display ```ftp-data``` untuk melihat data apa yang terkirim

<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20174407.png" >

**Soal 9**

Langkah Pertama Download dan unzip file nya untuk itu saya membuat script untuk melakukannya secara otomatis
```
#!/bin/bash

apt update && apt install -y wget unzip

KITAB_URL="https://drive.google.com/uc?export=download&id=11ua2KgBu3MnHEIjhBnzqqv2RMEiJsILY"
KITAB_ZIP="/root/kitab_penciptaan.zip"

wget --no-check-certificate -O "$KITAB_ZIP" "$KITAB_URL"

echo "Mengekstrak Kitab Penciptaan..."
mkdir -p /root/extracted_kitab
unzip -o "$KITAB_ZIP" -d /root/extracted_kitab/ 2>/dev/null

echo "Isi file ZIP:"
find /root/extracted_kitab/ -type f | while read file; do
echo " - $file ($(du -h "$file" | cut -f1))"
done

find /root/extracted_kitab/ -type f | head -1 | xargs -I {} cp {} /shared/kitab_penciptaan.txt
```
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%20" >


Selanjutnya mengubah user Ainur menjadi readonly saya juga mennggunkan script otomatis

```
#!/bin/bash

echo "=== MENGUBAH AKSES USER AINUR  ==="

pkill vsftpd

cat > /etc/vsftpd.conf << 'EOF'
listen=YES
listen_ipv6=NO
anonymous_enable=NO
local_enable=YES
write_enable=NO
local_umask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=NO
allow_writeable_chroot=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
ssl_enable=NO
local_root=/shared
EOF

/usr/sbin/vsftpd /etc/vsftpd.conf &

sleep 3

echo "Konfigurasi vsftpd saat ini:"
grep "write_enable" /etc/vsftpd.conf

echo "Status FTP service:"
netstat -tulpn | grep :21 && echo "✓ FTP service berjalan" || echo "✗ FTP service tidak berjalan"

echo ""
echo "=== AKSEŚ AINUR SEKARANG READ-ONLY ==="
```
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20221756.png" >
<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20171846.png" >

Lalu di buka gns3 lakukan klik kanan di kabel yang menghubungkan eru dengan manwe plih start capture untuk menganalisa di wireshark

Lanjut di manwe download ftp ```apt update && apt install -y ftp```

lalu jalankan ```ftp -nv 10.65.1.1``` untuk masuk ke ftp server 
lalu ketikan```user ainur 123``` untuk masuk ke user untuk download ketik ```get kitab_penciptaan.txt /root/kitab_di_manwe.txt```

<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20221816.png" >

di wireshark gunakan filter display ```ftp || tcp.port == 21``` untuk menampilakan aktivitas FTP

<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20221510.png" >

**Soal 10**
Di node Melkor buat script ototmati melakukan ping ,ping pertama sebanyak 10 lalu ping kedua sebanyak 100

```
#!/bin/bash

echo "=== SERANGAN PING FLOOD DARI MELKOR KE ERU ==="
echo "Target: 10.65.1.1 (Eru)"
echo "Jumlah paket: 100"
echo ""


START_TIME=$(date +%s)
echo "Waktu mulai: $(date)"

echo ""
echo "1. TEST KONEKSI NORMAL (10 paket):"
echo "----------------------------------"
ping -c 10 10.65.1.1

echo ""
echo "2. SERANGAN PING FLOOD (100 paket):"
echo "-----------------------------------"

ping -c 100 -i 0.1 10.65.1.1 | tee /root/ping_attack_results.txt


END_TIME=$(date +%s)
DURATION=$((END_TIME - START_TIME))

echo ""
echo "3. STATISTIK SERANGAN:"
echo "---------------------"
echo "Durasi serangan: $DURATION detik"


if [ -f "/root/ping_attack_results.txt" ]; then
    echo "Hasil serangan:"
    echo "==============="


    PACKET_LOSS=$(grep "packet loss" /root/ping_attack_results.txt | awk '{print $6}')
    echo "Packet Loss: $PACKET_LOSS"


    RTT_STATS=$(grep "rtt" /root/ping_attack_results.txt)
    if [ ! -z "$RTT_STATS" ]; then
        echo "RTT Statistics: $RTT_STATS"
    else
        echo "RTT Statistics: Tidak tersedia"
    fi


    PACKETS_SENT=$(grep "transmitted" /root/ping_attack_results.txt | awk '{print $1}')
    PACKETS_RECEIVED=$(grep "transmitted" /root/ping_attack_results.txt | awk '{print $4}')
    echo "Paket dikirim: $PACKETS_SENT"
    echo "Paket diterima: $PACKETS_RECEIVED"

    if [ ! -z "$PACKETS_SENT" ] && [ ! -z "$PACKETS_RECEIVED" ]; then
        SUCCESS_RATE=$((PACKETS_RECEIVED * 100 / PACKETS_SENT))
        echo "Success Rate: $SUCCESS_RATE%"
    fi
fi

echo ""
echo "=== SERANGAN SELESAI ==="
```
<img width="1917" height="816" alt="image" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20224802.png">

Sebelum melakukan serangn pergi ke Gns3 klik kanan kabel yang menghubungaan melkor dan eru lalu plih start capture
stelah serangan selesai cek wireshark menggunakan filter display ``` icmp || icmpv6```

<img width="1917" height="816" alt="image" src="https://github.com/user-attachments/assets/98fbf2dc-bf2c-4b02-9e10-17f41717c680" />

lalu membuat script otomatis mnengecek apakah ada paket loss

```
#!/bin/bash

echo "=== ANALISIS PASCA SERANGAN ==="

echo "1. HASIL SERANGAN PING:"
echo "======================="
if [ -f "/root/ping_attack_results.txt" ]; then
    cat /root/ping_attack_results.txt | tail -10
else
    echo "File hasil tidak ditemukan"
fi

echo ""
echo "2. PENGARUH TERHADAP KINERJA ERU:"
echo "================================"

echo "CPU Usage setelah serangan:"
top -bn1 | grep "Cpu(s)" | awk '{print "CPU: " $2 "% user, " $4 "% system, " $8 "% idle"}'

echo ""
echo "Memory Usage setelah serangan:"
free -h | grep -E "Mem|Swap"

echo ""
echo "Network Statistics:"
ip -s link show eth1 | grep -E "RX|TX" | head -4

echo ""
echo "3. ANALISIS PACKET LOSS DAN RTT:"
echo "================================"

if [ -f "/root/ping_attack_results.txt" ]; then
    LOSS_PERCENT=$(grep "packet loss" /root/ping_attack_results.txt | grep -o "[0-9]*%")
    AVG_RTT=$(grep "rtt" /root/ping_attack_results.txt | awk -F'/' '{print $5 " ms"}' 2>/dev/null)
    MIN_RTT=$(grep "rtt" /root/ping_attack_results.txt | awk -F'/' '{print $3 " ms"}' 2>/dev/null)
    MAX_RTT=$(grep "rtt" /root/ping_attack_results.txt | awk -F'/' '{print $7 " ms"}' 2>/dev/null)
    
    echo "Packet Loss: $LOSS_PERCENT"
    echo "RTT Minimum: $MIN_RTT"
    echo "RTT Rata-rata: $AVG_RTT" 
    echo "RTT Maksimum: $MAX_RTT"
    
    echo ""
    echo "4. KESIMPULAN DAMPAK SERANGAN:"
    echo "=============================="
    
    if [ "$LOSS_PERCENT" = "0%" ]; then
        echo "✓ Tidak ada packet loss - Eru masih stabil"
    else
        echo "✗ Terjadi packet loss $LOSS_PERCENT - Eru mengalami gangguan"
    fi
    
    if [ ! -z "$AVG_RTT" ]; then
        RTT_VALUE=$(echo $AVG_RTT | sed 's/ ms//')
        if (( $(echo "$RTT_VALUE > 10" | bc -l 2>/dev/null || echo "0") )); then
            echo "⚠ RTT tinggi ($AVG_RTT) - Kemungkinan ada congestion"
        else
            echo "✓ RTT normal ($AVG_RTT) - Kinerja jaringan baik"
        fi
    fi
fi

echo "=== ANALISIS SELESAI ==="
```

<img width="1917" height="816" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20224856.png">







**Soal 14** 

a. How many packets are recorded in the pcapng file?

Format: int

```> 500358```
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/user-attachments/assets/fe6e21bb-2007-4153-bc4e-3bb1d303b0fa" />

b. What are the user that successfully logged in?

Format: user:pass

```> n1enna:y4v4nn4_k3m3nt4r1```
- Filter dengan **HTTP** 
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 22 01 23" src="https://github.com/user-attachments/assets/fbb6756b-935f-4422-9089-2d194fb36b4d" />
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 22 01 42" src="https://github.com/user-attachments/assets/84eb8a1c-5bd9-4530-8f86-184295fbd63f" />

c. In which stream were the credentials found?

Format: int

```> 41824```

d. What tools are used for brute force?

Format: Hydra v1.8.0-dev

```> Fuzz Faster U Fool v2.1.0-dev```

**Soal 15**

a. What device does Melkor use?

Format: string

```> USB Keybord```
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 22 50 15" src="https://github.com/user-attachments/assets/d2d64bce-a4b6-4cfa-9e55-01b32659a3b3" />

b. What did Melkor write?

Format: string

```> UGx6X3ByMHYxZGVfeTB1cl91czNybjRtZV80bmRfcDRzc3cwcmQ=```

c. What is Melkor's secret message?

Format: string

```> Plz_pr0v1de_y0ur_us3rn4me_4nd_p4ssw0rd```

```Congratulations! Here is your flag: KOMJAR25{K3yb0ard_W4rr10r_uCB8ZzhA0urwDln4pDAIkH1On}```

**Soal 16**

a. What credential did the attacker use to log in?

Format: user:pass

```> ind@psg420.com:{6r_6e#TfT1p```
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 22 52 46" src="https://github.com/user-attachments/assets/b18d543f-1046-40fb-a6bb-32e29fa97dd5" />
<img width="1470" height="956" alt="Screenshot 2025-09-30 at 22 52 50" src="https://github.com/user-attachments/assets/89012554-c77b-4683-b727-fe4c2b6482f6" />

b. How many files are suspected of containing malware?

Format: int

```> 5```

c. What is the hash of the first file (q.exe)?

Format: sha256

<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 07 04" src="https://github.com/user-attachments/assets/0e6334a0-a5b3-4999-9aec-45ddace31976" />
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 07 13" src="https://github.com/user-attachments/assets/1db0dbb0-1573-48e3-8f8b-f98e237393bb" />
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 08 05" src="https://github.com/user-attachments/assets/6c9f5e2e-fd15-4317-9461-94bf41377e02" />

```_ws.col.info == "FTP Data: 1274 bytes (PASV) (SIZE q.exe)"```

```> ca34b0926cdc3242bbfad1c4a0b42cc2750d90db9a272d92cfb6cb7034d2a3bd```

d. What is the hash of the second file (w.exe)?

Format: sha256

```> 08eb941447078ef2c6ad8d91bb2f52256c09657ecd3d5344023edccf7291e9fc```

e. What is the hash of the third file (e.exe)?

Format: sha256

```> 32e1b3732cd779af1bf7730d0ec8a7a87a084319f6a0870dc7362a15ddbd3199```

f. What is the hash of the fourth file (r.exe)?

Format: sha256

```> 4ebd58007ee933a0a8348aee2922904a7110b7fb6a316b1c7fb2c6677e613884```

g.What is the hash of the fifth file (t.exe)?

Format: sha256

```> 10ce4b79180a2ddd924fdc95951d968191af2ee3b7dfc96dd6a5714dbeae613a```

```Congratulations! Here is your flag: KOMJAR25{Y0u_4r3_4_g00d_4nalyz3r_TuJ7hjo4hVEzZN1ZuwVpdVo5F}```

**Soal 17**

a. What is the name of the first suspicious file?

Format: file.exe
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 09 46" src="https://github.com/user-attachments/assets/bd2a63b6-d713-49a7-b32e-696e799e7067" />
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 09 51" src="https://github.com/user-attachments/assets/59897b8d-0b73-4857-85bb-7b8e651bb98b" />

```> Invoice&MSO-Request.doc```

b. What is the name of the second suspicious file?

Format: file.exe

```> knr.exe```

c. What is the hash of the second suspicious file (knr.exe)?

Format: sha256

```> 749e161661290e8a2d190b1a66469744127bc25bf46e5d0c6f2e835f4b92db18```

```Congratulations! Here is your flag: KOMJAR25{M4ster_4n4lyzer_AVytsjOodtHs6zT2qY9FJTs4R}```

**Soal 18**

a. How many files are suspected of containing malware?

Format: int
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 10 54" src="https://github.com/user-attachments/assets/85d386c6-e486-4677-9319-cc4a10e25ab7" />
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 10 59" src="https://github.com/user-attachments/assets/ff99c0db-839e-46dc-b9b6-48937702e1fb" />

```> 2```

b. What is the name of the first malicious file?

Format: file.exe

```>d0p2nc6ka3f_fixhohlycj4ovqfcy_smchzo_ub83urjpphrwahjwhv_o5c0fvf6.exe```

c. Apa nama file berbahaya yang kedua?

Format: file.exe

```> oiku9bu68cxqenfmcsos2aek6t07_guuisgxhllixv8dx2eemqddnhyh46l8n_di.exe```

d. What is the hash of the first malicious file?

Format: sha256

```> 59896ae5f3edcb999243c7bfdc0b17eb7fe28f3a66259d797386ea470c010040```

e. What is the hash of the second malicious file?

Format: sha256

```> cf99990bee6c378cbf56239b3cc88276eec348d82740f84e9d5c343751f82560```

```Congratulations! Here is your flag: KOMJAR25{Y0u_4re_g0dl1ke_uOwvyM9rkhkQ9MaIXXryRic8s}```

**Soal 19**

a. Who sent the threatening message?

Format: string (name)

<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 15 44" src="https://github.com/user-attachments/assets/437bb4f4-d33c-4997-9c4f-6319848a4817" />
<img width="1470" height="956" alt="Screenshot 2025-10-01 at 21 15 52" src="https://github.com/user-attachments/assets/660b39b9-ab64-4126-93f3-26c15d400610" />

```> Your Life```

b. How much ransom did the attacker demand ($)?

Format: int

```> 1600```

c. What is the attacker's bitcoin wallet?

Format: string

```> 1CWHmuF8dHt7HBGx5RKKLgg9QA2GmE3UyL```

```Congratulations! Here is your flag: KOMJAR25{Y0u_4re_J4rk0m_G0d_5wIfDf0FydSt7mvUw1KJdboQt}```

**Soal 20**

a. What encryption method is used?

Format: string

```> TLS```

b. What is the name of the malicious file placed by the attacker?

Format: file.exe

<img width="1470" height="956" alt="Screenshot 2025-10-04 at 23 58 39" src="https://github.com/user-attachments/assets/fdb3daa7-1478-4331-8b66-aa05c73e7fbd" />
<img width="1470" height="956" alt="Screenshot 2025-10-04 at 23 58 58" src="https://github.com/user-attachments/assets/52abdbea-5a1b-4612-a252-f7d25c0e6389" />
<img width="1470" height="956" alt="Screenshot 2025-10-04 at 23 59 37" src="https://github.com/user-attachments/assets/8e6b5abc-081c-4988-a4a1-13260be47803" />
<img width="1470" height="956" alt="Screenshot 2025-10-04 at 23 59 43" src="https://github.com/user-attachments/assets/3e52269e-8daf-43f9-961f-db43ebae7546" />

```> invest_20.dll```

c. What is the hash of the file containing the malware?

Format: sha256

<img width="1470" height="956" alt="Screenshot 2025-10-05 at 00 00 15" src="https://github.com/user-attachments/assets/14236ca1-15bb-453a-abbc-65d7f37f93a8" />

```> 31cf42b2a7c5c558f44cfc67684cc344c17d4946d3a1e0b2cecb8eb58173cb2f```

```Congratulations! Here is your flag: KOMJAR25{B3ware_0f_M4lw4re_hg5ARJOb8w6o3GnbxC1bSPqKg}```





















