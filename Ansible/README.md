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



# Ansible

![](https://img.shields.io/github/stars/pandao/editor.md.svg) ![](https://img.shields.io/github/forks/pandao/editor.md.svg) ![](https://img.shields.io/github/tag/pandao/editor.md.svg) ![](https://img.shields.io/github/release/pandao/editor.md.svg) ![](https://img.shields.io/github/issues/pandao/editor.md.svg) ![](https://img.shields.io/bower/v/editor.md.svg)

# Cara Main!

**NOTES :**
  - OS 1 : Ubuntu 16.04-Server as a worker
  - OS 2 : Debian 9-Server as a DB Server
  - Virtual Box for installing those 2 OS, and assuming you'd install it on them both already, let's move on~

**-- Prerequisites**
1. In the VM  (Ubuntu / Worker) install `openssh-server`, `ansible`, `sshpass` so you can connect into the VM thru SSH via your own PC.
```sh
$ sudo apt-get install openssh-server ansible sshpass
```

2. Then open up file `sshd_config` in `/etc/ssh/sshd_config`, and edit some code to match this line
```sh
    # Edit it / delete the word like -prohibit=password, and change it to yes
PermitRootLogin yes
RSAAuthentication yes
```

3. Run the ansible-playbook yaml file :)
```sh
$ ansible-playbook -vvv -i hosts master2.yml -k
```
4. If everything is success, there will be no '`failed`' task/things showed up~


![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/assets/master2%20-%201.png)

![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/assets/master2%20-%202.png)

**WORKER 1**

![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/assets/master2%20-%20worker1new.png)

**WORKER 2**
![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/assets/master2%20-%20worker2.png)

**Remote MariaDB / MySQL**
![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/assets/master2%20-%20mysqlremote.png)
***Select user , host from mysql.user;
![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/roles/db/usermysql.png)
***Show tables ;
![](https://raw.githubusercontent.com/hackazer/cloud-2018/master/Ansible/roles/db/tablesmysql.png)
