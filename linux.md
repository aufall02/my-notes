### Create symbolic link 
```bash
ln -s {path to the file or folder to be linked} {the path of the link to be created}
```
### Enable ssh acces for non root user
- create new user & set password
    ```bash
    sudo useradd -m {nama_user}
    sudo passwd
    ```
- pindahkan user ke group sudo untuk mendapatkan akses seperti root
  ```bash
  usermod -aG sudo {nama_user}
  ```
- pindah ke user yang sudah dibuat tadi, disini menggukan sheel bash
  ```bash
  su -s /bin/bash {nama_user}
  ```
- buat folder untuk menyimpan configurasi ssh
  ```bash
   mkdir /home/{nama_user}/.ssh
  ```
- buat sebuah file didalam folder .ssh dengna nama authorized_keys untuk menyimpan public key dari komputer local
  ```bash
  nano /home/{nama_user}/.ssh/authorized_keys
  ```
- pastikan chmod dari file tadi hanya user yang bersangkutan yang mempunyai hak akses read & write 
  ```bash
   chmod 600 /home/{nama_user}/.ssh/authorized_keys
   # atau
   chmod u+rw,go-rwx /home/{nama_user}/.ssh/authorized_keys
  ```

- restart ssh diserver
  ```bash
  systemctl restart ssh
  ```
- sekrang coba akses server menggunakan user yagn sudah dibuat tadi
  ```bash
    ssh {nama_user}@{ip_server}
  ```

#### Note

Jika terjadi eror saat mengakses server silahkan cek ```/var/log/secure``` menggunakann user root. jika terdapat pesan tentang tidak ada di AllowUsers, maka edit file ```/etc/ssh/sshd_config``` lalu tambahkan nama user di bagian AllowUsers.


### Disable ssh root login
- buka file ```sshd_config```
  ```bash
  nano /etc/ssh/sshd_config
  ```
- edit file ```sshd_config```
  ```bash
  PermitRootLogin no #secara default akan yes
  ```
- restart ssh service
  ```bash
  systemctl restart ssh
  ```



## Referensi
- [Dillion Megida - symslink linux](https://www.freecodecamp.org/news/symlink-tutorial-in-linux-how-to-create-and-remove-a-symbolic-link/)
- [Digital ocean - enable access ssh for non-root user](https://www.digitalocean.com/community/questions/how-to-enable-ssh-access-for-non-root-users)
- [Digital ocean - add an additional user with ssh key access](https://www.digitalocean.com/community/questions/i-want-to-add-an-additional-user-with-ssh-key-access)