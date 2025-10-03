# Jarkom-Modul-1-2025-K03

**Soal 1**

Membuat topologi sesuai soal, 2 switch dan 4 client
<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20164406.png" />

**Soal 2**

Menmbahkan NAT dan menyetting iptables di Router ERU 

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16
```

<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165315.png" />


**Soal 3**

Untuk memastikan bahwa setiap client dapat terhubung gunakan comand ping di ikuti ip tujuan

<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20162435.png" />

**Soal 4**

Agar setiap client bisah terhubung di internet yang bukan lokal tambahkan 

```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Untuk setiap client lalu lakukan uji coba dengn
```
ping google.com || apakah ada paket yang loss
```

<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20162515.png" />

**Soal 5**

Agar Konfigurasi yang sudah di lakukan tidak hilang kita bisa menyimpanyna di folder /root

<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165315.png" />
<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20165448.png" />


**Soal 6**

langakah pertama download dan unzip file saya menggunkan script .sh untuk meakukannya secara otomatis
```
#!/bin/bash
wget --no-check-certificate "https://docs.google.com/uc?export=download&id=1bE3kF1Nclw0VyKq4bL2VtOOt53IC7lG5">unzip traffic.zip
chmod +x traffic.sh
./traffic.sh
```
<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-03%20170232.png" >

sebelum melakukan run ```traffic.sh``` buka Gns3 dan klik kanan lalu lakukan start capture
untuk melakukan anlisa jaringan, jika sudah lakukan filter display 

```
ip.addr == 10.65.1.3
```

<img  width="1470" height="956" alt="Screenshot 2025-09-30 at 21 59 24" src="https://github.com/Dinarhmdn/Jarkom-Modul-1-2025-K03/blob/main/images/Screenshot%202025-10-01%20164956.png" >

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

```> invest_20.dll```

c. What is the hash of the file containing the malware?

Format: sha256

```> 31cf42b2a7c5c558f44cfc67684cc344c17d4946d3a1e0b2cecb8eb58173cb2f```

```Congratulations! Here is your flag: KOMJAR25{B3ware_0f_M4lw4re_hg5ARJOb8w6o3GnbxC1bSPqKg}```





















