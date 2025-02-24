# Tutorial Deploy di Proxmox
---
###### Halo! Selamat datang di panduan deployment Proxmox VE. Platform virtualisasi open-source yang handal dan gratis ini ideal untuk mengelola VM dan kontainer. Kami akan memandu Anda melalui instalasi, konfigurasi dasar, serta pembuatan dan pengelolaan VM.

## 📌 Prerequisites
---
##### Sebelum memulai, pastikan kamu memiliki:
- Pastikan Anda memiliki minimal 2GB RAM, tetapi 8GB atau lebih sangat disarankan.
- Minimal 32GB ruang penyimpanan diperlukan.
- Unduh file ISO Proxmox VE terbaru dari situs web resmi Proxmox.
- Siapkan nama domain yang memenuhi syarat (FQDN) untuk server.
- Pastikan Anda memiliki jaringan yang berfungsi. Jika server tidak terhubung ke internet, Anda tidak akan dapat memperbarui atau mengupgrade sistem Proxmox.

Setelah menginstal Proxmox VE, ingatlah untuk memperbarui sistem menggunakan apt update dan apt dist-upgrade.

---

📌 Sebelum kita mulai dengan langkah-langkah praktis, pastikan Anda sudah mempersiapkan semua peralatan dan bahan yang dibutuhkan. Dengan begitu, proses pembelajaran ini akan lebih lancar dan efektif
Sekarang, mari kita mulai dengan langkah pertama!

## Langkah Pertama (Membuat Container)

![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/gambar-1.png?raw=true)

1.Pilih Node: Pada panel sebelah kiri, di bawah "Datacenter", pilih node Proxmox tempat Anda ingin membuat CT. Node ini biasanya memiliki nama seperti "pg-proxmoxlab" seperti pada gambar.
2.Klik "Create CT": Setelah memilih node, cari dan klik tombol "Create CT". Tombol ini biasanya terletak di bagian atas antarmuka, di sebelah tombol "Create VM".
3.Wizard Pembuatan CT: Setelah mengklik "Create CT", sebuah wizard akan muncul untuk memandu Anda melalui proses pembuatan CT. Wizard ini biasanya terdiri dari beberapa tab atau bagian:
- General: Di sini, Anda akan memasukkan informasi dasar tentang CT Anda, seperti:
    - ![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/gambar-2.png?raw=true)
        - Node: (Seharusnya sudah terpilih).
        - CT ID: ID unik untuk CT Anda (misalnya, 100, 101, dll.).
        - Hostname: Nama host untuk CT Anda.
        - Password: Kata sandi untuk akun root di dalam CT.
        - Template: Pilih template OS yang ingin Anda gunakan untuk CT Anda. Template adalah image dasar dari sistem operasi yang akan diinstal di dalam CT. Anda dapat memilih dari daftar template yang tersedia atau mengunggah template Anda sendiri.
        ![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/template.png?raw=true)
        - Storage: Pilih storage pool atau lokasi tempat CT Anda akan disimpan.
        ![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/storage.png?raw=true)
        - Network: Konfigurasi jaringan untuk CT Anda. Anda dapat memilih untuk menggunakan DHCP atau mengkonfigurasi alamat IP statis.
        ![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/network.png?raw=true)
        - CPU: Alokasikan core CPU untuk CT Anda.
        - Memory: Alokasikan RAM untuk CT Anda.
    

4.Konfirmasi dan Buat: Setelah Anda selesai mengkonfigurasi semua opsi, tinjau ringkasan konfigurasi Anda. Jika semuanya sudah benar, klik tombol "Create" atau "Finish" untuk membuat CT.
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/confirm.png?raw=true)
5.Mulai CT: Setelah CT dibuat, Anda dapat menemukannya di daftar VM/CT di bawah node Anda. Pilih CT yang baru dibuat, dan klik tombol "Start" untuk memulai CT.
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/start.png?raw=true)
6.Konsol CT: Setelah CT berjalan, Anda dapat mengakses konsol CT dengan memilih CT dan mengklik tombol "Console". Ini akan membuka jendela konsol di mana Anda dapat berinteraksi dengan CT Anda.
---
## Langkah Kedua (Mengakses dan menggunakan CT yang Baru Dibuat)
1.Mulai Container:
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/start.png?raw=true)
- Pilih CT yang baru saja Anda buat dari daftar di panel kiri. Pada gambar, terlihat CT dengan ID 124 (naufalardzi) sudah terpilih.
- Klik tombol "Start" yang terletak di bagian atas antarmuka. Ini akan memulai proses booting CT. Anda dapat melihat status "OK" pada log tugas di bagian bawah, yang menandakan CT berhasil dimulai.

2.Buka Konsol: 
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/interaksi-konsol.png?raw=true)
- Setelah CT berjalan, klik tombol "Console" yang terletak di sebelah tombol "Start" dan "Shutdown". Ini akan membuka jendela konsol, memungkinkan Anda untuk berinteraksi langsung dengan sistem operasi di dalam CT.

3.Login ke Sistem:
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/login.jpg?raw=true)
- Di jendela konsol, Anda akan melihat prompt login. Pada gambar, terlihat tulisan "naufalardzi login:".
- Masukkan username dan password yang Anda konfigurasi saat membuat CT. Biasanya, Anda akan login sebagai user root dengan password yang sudah Anda tentukan sebelumnya.

4.Mulai Menggunakan CT:
- Setelah berhasil login, Anda memiliki akses penuh ke command line CT. Anda dapat mulai menginstal software, mengkonfigurasi sistem, dan menjalankan aplikasi sesuai kebutuhan Anda.
---

## Langkah Ketiga (Konfigurasi dan Verifikasi Jaringan CT)
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/gambar-3.png?raw=true)

1.Periksa Konfigurasi: Pastikan IP statis, gateway, dan DNS di file 01-network-manager-all.yaml sudah benar.
2.Simpan: Ctrl+O, Enter, lalu Ctrl+X untuk menyimpan dan keluar dari nano.
3.Restart Jaringan: sudo systemctl restart networking atau sudo reboot.
4.Uji Koneksi: ping 192.168.50.1 (gateway) lalu ping. Pastikan semua perintah dijalankan di dalam konsol CT.
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/ping.png?raw=true)
---

## Langkah Keempat(Mengelola Website di CT Anda)
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/gambar-4.png?raw=true)

1.Memastikan Apache Berjalan: Anda sebelumnya menjalankan systemctl restart apache2. Ini adalah langkah penting. Pastikan Apache berjalan dengan baik. Anda bisa memeriksanya dengan: 
- systemctl status apache2
Jika Apache tidak berjalan, coba jalankan 'sudo systemctl start apache2'.

2.Memahami Struktur Direktori Website:
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/direktori.png?raw=true)
- /var/www/html/: Ini adalah direktori default untuk menyimpan file website Anda.
- /var/www/html/portoezi/: Ini adalah subdirektori yang berisi file website Anda. Gambar menunjukkan file seperti assets, index.html, mediaqueries.css, script.js, dan style.css.
- /etc/apache2/sites-available/: Ini adalah direktori tempat file konfigurasi virtual host Apache disimpan. File-file ini menentukan bagaimana Apache menghost website yang berbeda.

3.Mengedit Konfigurasi Virtual Host (Jika Diperlukan)
- Anda sebelumnya mencoba mengedit 000-default.conf. File ini adalah konfigurasi virtual host default. Dalam banyak kasus, Anda mungkin perlu membuat file konfigurasi virtual host terpisah untuk website Anda.
- Jika Anda perlu membuat file konfigurasi virtual host baru:
    - Buat file baru, misalnya portoezi.conf di direktori /etc/apache2/sites-available/.
    - Salin isi dari 000-default.conf ke portoezi.conf.
    - Edit portoezi.conf untuk mencerminkan konfigurasi yang Anda inginkan, seperti:
        - DocumentRoot /var/www/html/portoezi (menentukan direktori website).
        - ServerName contohdomain.com (menentukan domain website).
    - Aktifkan virtual host baru: sudo a2ensite portoezi.conf.
    - Nonaktifkan virtual host default (jika perlu): sudo a2dissite 000-default.conf.
    - Restart Apache: sudo systemctl restart apache2.

4.Memverifikasi Website: 
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/ubuntu.jpeg?raw=true)
- Buka browser web dan kunjungi alamat IP CT Anda (misalnya, http://192.168.50.110).
- Jika Anda telah mengkonfigurasi domain, kunjungi domain tersebut (misalnya, http://contohdomain.com).
- Anda seharusnya melihat website Anda.
![alt text](https://github.com/arzisukajs/Tutorial-Deploy-Proxmox/blob/main/hasil.jpeg?raw=true)
