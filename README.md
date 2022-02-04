# **TUBES Report**

## Group 12 [IT02-01]

**Rifqi Naufal A 1202190012 || Andi Tadang P 1202190046**

<hr> 

Scheme :

https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/Final%20Project/assets/arsitektur.png

First we make container :

- 6 instance LXC ubuntu 20.04 PHP 7.4
```
    lxc-create -n lxc_php7_1 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php7_2 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php7_3 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php7_4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php7_5 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php7_6 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 2 instance LXC debian 10 PHP 5.6
```
    lxc-create -n lxc_php5_1 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
    lxc-create -n lxc_php5_2 -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

- 1 instance LXC debian 10 mariadb server
```
lxc-create -n lxc_db_server -t download -- --dist debian --release buster --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

  ![image](https://user-images.githubusercontent.com/93064971/152371641-bd6c06da-c466-4725-9c59-80a620007217.png)

- Setting all of containers auto start

  ![image](https://user-images.githubusercontent.com/93064971/152480230-ccf9847c-d930-4b1c-85ca-4828a892c222.png)

- Setting hosts and adding IP Address and Domain for each containers in VM ubuntu server 

  ![image](https://user-images.githubusercontent.com/93064971/152480271-9048233e-e7ae-48e8-918e-be2a720c394c.png)

- Configuration lxc_db_server, lxc_php5_1, lxc_php5_2, lxc_php7_1, lxc_php7_2, lxc_php7_3,  lxc_php7_4, lxc_php7_5 and lxc_php7_6 like this commands below

- Configuration lxc_db_server, lxc_php5_1, lxc_php5_2, lxc_php7_1, lxc_php7_2, lxc_php7_3,  lxc_php7_4, lxc_php7_5 and lxc_php7_6 like this commands below

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

- Setting password for lxc_db_server ssh, lxc_php5_1, lxc_php5_2, lxc_php7_1, lxc_php7_2, lxc_php7_3,  lxc_php7_4, lxc_php7_5 and lxc_php7_6

    ```markdown
    passwd (ex: 1)
    ```

- Log out from lxc_db_server, lxc_php5_1, and lxc_php5_2, lxc_php7_1, lxc_php7_2, lxc_php7_3,  lxc_php7_4, lxc_php7_5 and lxc_php7_6

    ```markdown
    exit
    ```

- Entering directory

    ```markdown
    cd ~/ansible/tubes
    ```

- Creating hosts and adding script



