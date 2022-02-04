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

![image](https://user-images.githubusercontent.com/93064971/152480551-5e9d0d4b-ee4f-4209-8abd-e9387a304224.png)

- Setting sites-available pada vm menggunakan nama kelompok12.fpsas dan symlink ke sites-enabled

![image](https://user-images.githubusercontent.com/93064971/152480797-8966920c-5050-4409-980e-53fd9ccb6e0c.png)

![image](https://user-images.githubusercontent.com/93064971/152480822-9b63fb4c-6e8e-4e72-b474-0f1038716ab5.png)

![image](https://user-images.githubusercontent.com/93064971/152480840-8e267b57-191c-433e-a155-c750e2729a36.png)

- Creating install-laravel.yml file and adding configuration

![image](https://user-images.githubusercontent.com/93064971/152480979-4d4ea627-b847-48c6-8ffb-377b49708aca.png)

- Creating directory roles/laravel, and creating tasks, handlers, templates in db directory

- nano roles/laravel/handlers/main.yml

![image](https://user-images.githubusercontent.com/93064971/152481115-107816ee-e304-47f4-8880-1bdf6656187a.png)

- nano roles/laravel/tasks/main.yml

![image](https://user-images.githubusercontent.com/93064971/152481291-26fc3fba-6bd3-4a86-b013-bc69de4e87f9.png)

![image](https://user-images.githubusercontent.com/93064971/152481320-b6378d42-877c-46ad-ba85-3cf9756c0f30.png)

![image](https://user-images.githubusercontent.com/93064971/152481333-a03f892d-6199-4aa8-97ff-080133ac026c.png)

![image](https://user-images.githubusercontent.com/93064971/152481361-f6bf5024-c07d-492f-98ae-baa688dbc052.png)

![image](https://user-images.githubusercontent.com/93064971/152481373-f1d9f70c-9f5e-4dd9-91b9-dd8149e956d9.png)

![image](https://user-images.githubusercontent.com/93064971/152481465-a7e6913f-8d7a-45b3-9b4b-7be51dbdf70e.png)

- nano roles/laravel/templates/landing

![image](https://user-images.githubusercontent.com/93064971/152481491-33a865e0-3df4-44aa-8f36-f71b1e2cc299.png)
