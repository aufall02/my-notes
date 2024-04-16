# setup php my admin


- Install php
    ```bash
     apt-get install php-fpm php-mysql
    ```
- Install mysql server
    ```bash
    apt install mysql-server
    mysql_secure_installation
    ```
- Install php myadmin
    ```bash
    cd /var/www/{domain_anda}/
    wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.zip

    apt install unzip
    unzip /var/www/{domain_anda}/phpMyAdmin-5.2.1-all-languages.zip
    # optional
    mv phpMyAdmin-5.2.1-all-languages/ phpMyAdmin

    ```
- ubah hak akses folder phpMyAdmin
  ```bash
  chown -R www-data:www-data /var/www/aufalls.tech/phpMyAdmin
  ```


- buat 1 file configurasi di site avaible nginx
  ```conf
  server {
    server_name {server_name};
    root /var/www/{domain}/phpMyAdmin;

    index index.php index.html index.htm;

    location /phpmyadmin {
        alias /var/www/{domain}/phpMyAdmin;
        index index.php;
    }

    client_max_body_size 100M;

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        # sesuaikan dengna versi php yang digunakan
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
  }
  ```
- cek konfigurasi && restart server
  ```bash
  sudo nginx -t && systemctl restart nginx
  ```
- akses ip server {ip_server}/phpmyadmin
- selanjutnya create user baru untuk masuk kedalam phpmyadmin
  ```bash
  mysql
  ```
  ```mysql
  CREATE USER "user01"@"localhost" IDENTIFIED BY "password";
  # hak akses untuk user
  GRANT ALL PRIVILEGES ON *.* TO 'aufal'@'localhost';
  # reload hak akses
  FLUSH PRIVILEGES;
  ```






## Referensi
- [Bagja lazwardi - bootcamp ramadhan](https://drive.google.com/drive/folders/1aBpNXJ41pyKJu4DRckEJvGI2mZ095fWa)