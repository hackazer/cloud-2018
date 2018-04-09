# Tugas Vagrant

![](https://blog.theodo.fr/wp-content/uploads/2017/07/Vagrant.png)

## Soal Sesilab Nginx

Buatlah sistem load balancing dengan 1 load balancer(nginx dan 2 worker(apache2), terapkan algoritma load balancing round-robin, least-connected, dan ip-hash.

Soal :

1. Buatlah Vagrantfile sekaligus provisioning-nya untuk menyelesaikan kasus.
2. Analisa apa perbedaan antara ketiga algoritma tersebut.
3. Biasanya pada saat membuat website, data user yang sedang login disimpan pada session. Sesision secara default tersimpan pada memory pada sebuah host. Bagaimana cara mengatasi masalah session ketika kita melakukan load balancing?

### Petunjuk

1. Lakukan soal nomor 1 dan dokumentasikan bagaimana cara setupnya pada laporan markdown.
2. Untuk nomor 2 dan 3 merupakan analisa terhadap suatu masalah, jawablah pertanyaan diatas dan tulis pada laporan.


## A. Cara Main
### 1. Install Vagrant 3 biji
	- Set up 3 Vagrant. 1 Load balancer + Worker.
	-- Pakai Ubuntu 16.04 (Xenial64)
	

### 2. Provisioning Install software
	- Load Balancer : 
		# apt-get install nginx -y
		# apt-get install php7.0-fpm -y

	- Worker :
		# apt-get install apache2
		# apt-get install libapache2-mod-php7.0 php7.0-fpm -y


### 3. Setup Worker ama Load Balancer nya
	- Worker : 
		Set up worker nya biar bisa baca file PHP. Edit file.conf berikut di kedua file .conf worker :

		SS PASTE Disini, fileconfig isi disini

	- Load Balancer :
		# Set up LB nya di file default di /etc/nginx/sites-available/ (yang sudah di SYMLINK) dengan tambahan kode berikut :

		ISI DISINI FILE CONFIGNYA
