# install postgresql & phppgadmin
:: version : - phppgadmin 7.13.0
             - postgres 14.11 
             - php 8.1.2
             - ubuntu 22.04

## instalasi
  ```bash
    sudo apt-get install postgresql postgresql-contrib phppgadmin php{php_verison}-fpm
    sudo su postgres createuser -P --interactive
    sudo ln -s /usr/share/phppgadmin /var/www/html/
  ```

## config
- nginx
  ```bash
    {
        ....
         location /phppgadmin {
                root /var/www/html/;
                index index.php;

         }
        ....
    }
  ```
- postgres
   
    lokasi : nano /etc/postgresql/{postgres_version}/main/postgresql.conf
    ```bash
    listen_addresses = '*'  
    ```
- phppgadmin
  
  lokasi : nano /etc/phppgadmin/config.inc.php
  ```bash
  # jika ingin login mengunakan user postgres, secara default ini dilarang
  $conf['extra_login_security'] = false;
  ```
- allow port pgsql agar bisa diakses di komputer lokal tampa mengguakan phppgadmin
  ```bash
  ufw allow {port_psotgres}
  ```


## Referensi
- [stack overflow - install postgres & phppgadmin](https://stackoverflow.com/questions/56642735/how-to-install-postgresql-and-phppgadmin-with-nginx)
- [alibaba cloud - setup prstgresql](https://www.alibabacloud.com/blog/how-to-set-up-postgresql-and-phppgadmin-on-ubuntu-18-04_595558)
- [stack overflow - psql can't connect to server](https://stackoverflow.com/questions/31645550/postgresql-why-psql-cant-connect-to-server)
- [stack overflow - disallow security](https://stackoverflow.com/questions/19204816/login-disallowed-for-security-reasons-postgresql-centos-server)