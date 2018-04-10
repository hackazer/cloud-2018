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


## 1. Cara Main
### 1.1. Install Vagrant 3 biji
	- Set up 3 Vagrant. 1 Load balancer + Worker.
		-- Edit pada Vagrantfile pada semua vagrant , bedakan ip_private masing - masing vagrant nya 		   seperti contoh berikut 
			-- load balancer : 
				# config.vm.network "private_network", ip: "192.168.0.2"
			-- Worker 1 dan 2 
				# config.vm.network "private_network", ip: "192.168.0.3"
				# config.vm.network "private_network", ip: "192.168.0.4"  
		-- Pakai Ubuntu 16.04 (Xenial64) untuk suport php 7
		-- Setting # config.vm.provision "shell", path: "bootstrap.sh"  
	
	

### 1.2. Provisioning Install software
	- Load Balancer : 
		# apt-get install nginx -y
		# apt-get install php7.0-fpm -y

	- Worker :
		# apt-get install apache2
		# apt-get install libapache2-mod-php7.0 php7.0-fpm -y


### 1.3. Setup Worker sama Load Balancer nya
	- Worker : 
		Set up worker nya biar bisa baca file PHP. Edit /etc/apache2/mods-enabled/ pada kedua worker menjadi :

		<IfModule mod_dir.c>
        	DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
		</IfModule>

	- Load Balancer :
		> Set up LB nya di file default di /etc/nginx/sites-available/ (yang sudah di SYMLINK) dengan tambahan kode berikut :

		> Tambahkan method untuk load balancing seperti berikut pada konfigurasi nginx di load balancer nya
			## ip_hash

				upstream workers {
			    ip_hash;
			    server 192.168.0.3;
			    server 192.168.0.4;
				}

			## least_conn

				upstream workers {
				    least_conn;
				    server 192.168.0.3;
				    server 192.168.0.4;
				}

			## round_robin 

				upstream workers {
				    server 192.168.0.3;
				    server 192.168.0.4;
				}

## 2. Analisa apa perbedaan load balancing round-robin, least-connected, dan ip-hash

### Round Robin 
	konsep dasar dari algoritma ini yaitu dengan menggunakan time sharing. membagi beban kerja sesuai antrian. misal ada 4 server, a b c d maka beban akan dibagi dari a - d kemudian balik lagi ke a sampai habis dibagikan. 

### Least Connection 
	konsep Least connection yaitu membagi beban kerja berdasarkan banyaknya koneksi yang sedang dilayani oleh sebuah server yang aktif. Algoritma penjadwalan ini termasuk dalam penjadwalan dinamik, dimana memerlukan perhitungan koneksi yang aktif untuk masing-masing real server. Misal, ada 2 server yaitu A dan B. Koneksi aktif pada server A berjumlah 2 koneksi, koneksi aktif pada server B berjumlah 5 koneksi, maka beban kerja akan diberikan kepada server A karena koneksi aktif server A lebih sedikit dibanding B.

### IP Hash 
	Menggunakan IP source dan destination dari klien dan server untuk men-generate hash key menjadi kode yang unik. Kode ini digunakan untuk mengalokasikan klien ke server tertentu. Metode ini dapat memastikan bahwa klien akan terhubung dengan server yang sama yang sebelumnya sudah terhubung. 

## 3. Bagaimana mengatasi sebuah session ketika kita melakukan load balancing?