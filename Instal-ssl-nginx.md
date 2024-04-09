# SSL - Nginx

## Open ssl 

### Instal open ssl untuk membuat self-signed SSL Certificate 

self-signed ssl certifikate adalah sertifikat ssl gratis yang dibuat dan ditandatangani oleh pembuatnya sendiri

### Membuat Self-Signed SSL Certificate

- install opensll

    ```bash
    sudo apt install openssl
    ```
- request file key dan sertifikat 
  
    ```bash
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
    ```
- membuat file dhparam.perm
  ```bash
  sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
  ```
### Konfigurasi Nginx SSL
- buat file untuk tempat konfigurasi file sertifikate yagn sudah dibuat
  
  ```bash
  # nano
  sudo nano /etc/nginx/snippets/self-signed.conf

  # vi
  sudo vi /etc/nginx/snippets/self-signed.conf
  ``` 

- salin path file key dan sertifikat yang sudah dibuat 
    
    ```bash
    ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
    ```
- buat file baru di dalam folder /etc/nginx/snippets untuk tempat konfigurasi ssl 
  ```bash
  # nano
  sudo nano /etc/nginx/snippets/ssl-params.conf
  
  # vi
  sudo vi /etc/nginx/snippets/ssl-params.conf
  ```
- masukkan kod konfigurasi berikut
  ```bash
    ssl_protocols TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_dhparam /etc/nginx/dhparam.pem;
    ssl_ciphers EECDH+AESGCM:EDH+AESGCM;
    ssl_ecdh_curve secp384r1;
    ssl_session_timeout  10m;
    ssl_session_cache shared:SSL:10m;
    ssl_session_tickets off;
    ssl_stapling on;
    ssl_stapling_verify on;
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;
    # Disable strict transport security for now. You can uncomment the following
    # line if you understand the implications.
    #add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
  ```
- edit file configurasi server 
  ```bash
  sudo nano /etc/nginx/sites-available/default
  #untuk file konfigurasi server sesuaikan dengan file yang sudah ada
  ```
  ```bash
  server {
    listen 443 ssl;
    listen [::]:443 ssl;
    include snippets/self-signed.conf;
    include snippets/ssl-params.conf;

    # lokasi file index web
    root /var/www/{web-name}/html;
            index index.html index.htm index.nginx-debian.html;

    # sesuaikan dengan nama server masing -masing
    server_name mydomain.com www.mydomain.com;

    location / {
                    try_files $uri $uri/ =404;
            }
    }

  server {
    listen 80;
    listen [::]:80;

    server_name domainanda.com www.domainanda.com;

    return 302 https://$server_name$request_uri;
  }
  ```
### Setup Firewall

menggunakan ufw

- install ufw
  
  ```bash
   sudo apt install ufw
  ```
- Setting Up Default Policies
  
  ```bash
  sudo ufw default deny incoming
  sudo ufw default allow outgoing
  ```
- membuka akses untuk ssh
  ```bash
  sudo ufw allow OpenSSH
  sudo ufw allow ssh
  sudo ufw allow 22
  udo ufw allow 2222
  ```
- cek akses apa saja yang kita buka
  ```bash
  sudo ufw show added
  ```
- aktifkan ufw
  ```bash
  sudo ufw enable
  # cek status ufw
  sudo ufw status
  ```
- membuka akses untuk https
    ```bash
    sudo ufw allow 'Nginx Full'
    sudo ufw delete allow 'Nginx HTTP'
    ```
### Mengaktifkan Perubahan Konfigurasi Nginx SSL
- pastikan tidak ada eror dek file configurasi nginx
  ```bash
  sudo nginx -t
  ```
- restrat nginx
  ```bash
  sudo systemctl restart nginx
  ```
### Testing
- buka halaman browser dan masukkan 
  ```bash
  https://ip-server
  ```

## Referensi
 * [niaga hoster - install ssl-nginx](https://www.niagahoster.co.id/blog/install-nginx-ssl/)
 * [digital ocean - setup firewal ufw](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu)