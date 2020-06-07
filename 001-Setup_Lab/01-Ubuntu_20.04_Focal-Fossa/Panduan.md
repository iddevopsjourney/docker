# Setup Lab Docker - VirtualBox - OS Linux Ubuntu 20.04 Focal Fossa
Flow untuk setup lab docker adalah sebagai berikut :
<p><img src="https://github.com/iddevopsjourney/docker/blob/master/001-Setup_Lab/01-Ubuntu_20.04_Focal-Fossa/images/SetupLabDocker-VirtualBox.png"></p></br>

Laptop yang digunakan adalah Lenovo Thinkpad X230 (lumayan berumur) dengan spesifikasi sebagai berikut :
- Prosesor Core i5
- RAM 12 GB
- Disk HDD
- OS Windows 7

Tools pendukung dapat diperoleh di :
- VirtualBox : https://www.virtualbox.org/
- Image Linux Ubuntu 20.04 Focal Fossa : https://www.osboxes.org/ubuntu/

### VirtualBox setup
Konfigurasi spesifikasi VM di virtualbox :
- CPU : 2 Core
- RAM : 16 GB
- DISK : 10 GB
- Network : Bridge

### Konfigurasi Linux Ubuntu 20.04 Focal Fossa
Saat first start linux pertama kali dilakukan konfigurasi :
1. Update OS Linux
```script
$ sudo apt update
$ suo apt upgrade
```
2. IP Address di setting menjadi static
```script
$ cat /etc/cloud/cloud.cfg.d/subiquity-disable-cloudinit-networking.cfg
network: {config: disabled}
$

$ ip add show

// Perubahan konfigurasi dari DHCP ke Stati IP
$ sudo vi /etc/netplan/00-installer-config.yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: true
  version: 2

// Menjadi
network:
  ethernets:
    enp0s3:
      addresses: [192.168.1.3/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [4.2.2.2, 8.8.8.8]
  version: 2

// apply konfigurasi 
$ sudo netplan apply

// Verifikasi konfigurasi
$ ip add show
$ ip route show
```
3. Konfigurasi Remote SSH
```script
$ sudo apt-get install ssh
$ sudo systemctl enable --now ssh
$ sudo systemctl status ssh
```
### Snapshoot
Snapshoot pada stage ini agar mempermudah proses roolback dan vm dapat digunakan untuk lab yang berbeda - beda sesuai kebutuhan.

### Penutup
Persiapan lab telah selesai dan siap untuk memulai belajar docker.
