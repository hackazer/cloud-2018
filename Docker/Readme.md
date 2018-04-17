# Tugas Vagrant

![](https://logz.io/wp-content/uploads/2016/01/docker-facebook.png)

## Soal Sesilab Docker

Memanfaatkan Docker untuk Load Balancing (?)


## A. Cara Main
### 1. Install Docker pastinya, 
	- Sudo apt-get install docker atau docker-ce
	

### 2. Buat Dockerfile sesuai kebutuhan
- **Dockerfile 1** : Untuk Web Python Flask nya
		
>FROM ubuntu:16.04
>
>RUN apt-get install python-pip (ini kalau pip nya belum ada hehe)
>
>RUN apt update && apt install -y wget apt-utils zip python2.7 python-pip
>RUN apt install -y libmysqlclient-dev
>RUN pip install --upgrade pip
>
>RUN wget https://cloud.fathoniadi.my.id/reservasi.zip && unzip reservasi.zip
>
>WORKDIR reservasi
>RUN pip install -r req.txt
>
>CMD python server.py
>
>EXPOSE 80

**Buat image dengan command** :	`docker build -t reservasi`

- **Dockerfile 2** : Untuk setup MySQL


```
FROM mysql:5.7
ENV MYSQL_ROOT_PASSWORD passwordawan
ENV MYSQL_USER userawan
ENV MYSQL_PASSWORD buayakecil
ENV MYSQL_DATABASE reservasi`

COPY ./reservasi.sql /docker-entrypoint-initdb.d
```

**Buat image dengan perintah** :  `docker build -t mysql_reservasi`

#### Membuat file `docker-compose.yml`
> Set untuk worker, balancer nya disini

```
lorem ipsum hehehe
Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.
```










`