# **TUBES Report**

## Group 12 [IT02-01]

**Rifqi Naufal A 1202190012 || Andi Tadang P 1202190046**

<hr> 

Scheme :

https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/Final%20Project/assets/arsitektur.png

First we make container :

- 6 instance LXC ubuntu 20.04 PHP 7.4
```
sudo lxc-create -n ubuntu_php7.4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n ubuntu_php7.4_2 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n ubuntu_php7.4_3 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n ubuntu_php7.4_4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n ubuntu_php7.4_5 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n ubuntu_php7.4_6 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 2 instance LXC debian 10 PHP 5.6
```
sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
sudo lxc-create -n debian_php5.6_2 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 1 instance LXC debian 10 mariadb server
```
sudo lxc-create -n lxc_mariadb -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

![image](https://user-images.githubusercontent.com/93064971/152371641-bd6c06da-c466-4725-9c59-80a620007217.png)

- Setting all of containers auto start

    ```markdown
    echo "lxc.start.auto = 1" >> /var/lib/lxc/lxc_mariadb/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/debian_php5.6/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/debian_php5.6_2/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4_2/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4_3/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4_4/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4_5/config
    echo "lxc.start.auto = 1" >> /var/lib/lxc/ubuntu_php7.4_6/config
    ```
- Setting hosts and adding IP Address and Domain for each containers in VM ubuntu server 

![image](https://user-images.githubusercontent.com/93064971/152372435-a08c1609-9f21-4655-ab95-57f575f423e8.png)

- Configuration lxc_mariadb, debian_php5.6, debian_php5.6_2, ubuntu_php7.4, ubuntu_php7.4_2, ubuntu_php7.4_3, ubuntu_php7.4_4, ubuntu_php7.4_5 and ubuntu_php7.4_6 like this       commands below

- Install ssh server

    ```markdown
    apt install openssh-server
    ```

- Adding configuration at /etc/ssh/sshd_config

    ```markdown
    nano /etc/ssh/sshd_config
    
    # setting config
    PermitRootLogin yes
    RSAAuthentication yes
    ```

- Restart ssh server

    ```markdown
    service sshd restart
    ```

- Setting password for lxc_mariadb, debian_php5.6, debian_php5.6_2, ubuntu_php7.4, ubuntu_php7.4_2, ubuntu_php7.4_3, ubuntu_php7.4_4, ubuntu_php7.4_5 and ubuntu_php7.4_6

    ```markdown
    passwd (ex: 1)
    ```

- Log out from lxc_mariadb, debian_php5.6, debian_php5.6_2, ubuntu_php7.4, ubuntu_php7.4_2, ubuntu_php7.4_3, ubuntu_php7.4_4, ubuntu_php7.4_5 and ubuntu_php7.4_6

    ```markdown
    exit
    ```

- Entering directory

    ```markdown
    cd ~/ansible/tubes
    ```

ansible hosts

![image](https://user-images.githubusercontent.com/93064971/152370357-39b7a8d2-ec1b-4462-b77f-be31b37563a4.png)

install-ci.yml

![image](https://user-images.githubusercontent.com/93064971/152370626-f345a47c-ace0-4d87-abc7-42408c343e29.png)

install-laravel.yml

![image](https://user-images.githubusercontent.com/93064971/152370846-47bd5919-c131-47a6-b18e-8ad746fca5a8.png)

install-wp.yml

![image](https://user-images.githubusercontent.com/93064971/152371010-a604fcbe-4c61-4fc9-a11f-a5f6cb7bc89d.png)

