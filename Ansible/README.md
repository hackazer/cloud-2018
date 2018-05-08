## Soal

1. Buat 3 VM, 2 Ubuntu 16.04 sebagai worker, 1 Debian 9 sebagai DB server
2. Pada vm Debian install Mysql dan setup agar koneksi DB bisa diremote dan memiliki user:
    username: regal
    password: bolaubi

3. Pada worker:
    2.1. Install Nginx
    2,2, Install PHP 7.2
    2.3. Install composer
    2.4. Install Git

    dan pastikan worker dapat menjalankan Laravel 5.6
    
4. Clone [https://github.com/udinIMM/Hackathon](https://github.com/udinIMM/Hackathon) pada setiap worker dan setup database pada .env mengarah ke DB server.

5. Setup root directory nginx ke folder Laravel hasil clone repo diatas