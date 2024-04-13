# Install fish
- add fish shell repository
  ```bash
  sudo apt-add-repository ppa:fish-shell/release-3
  ```
- Update and Upgrade Repository Packages
    ```bash
    sudo apt-get update && sudo apt-get upgrade
    ```
- Install Fish Shell
    ```bash
    sudo apt-get install fish
    ```


# Set Fish Shell as the Default Shell
- buka file chsh
 
    ```bash
    sudo nano /etc/pam.d/chsh
    ```
- masukkan ```#``` didepan line ```auth required pam_shells.so``` 
- simpan hasil perubahan 
- jalankan perintah 
    ```bash
    sudo chsh -s $(which fish)
    ```
- buka lagi file chsh
- hapus tanda ```#``` dipan line ```auth required pam_shells.so``` 
- save 

## Test

```bash
sudo -i
```

## Referensi
* [medium - saad jamil - isntall & setup fish](https://medium.com/@saadjamilakhtar/how-to-install-and-set-up-the-fish-shell-b9e0ddb12cc9)
* [askubuntu - fish shell as default](https://askubuntu.com/questions/848030/fish-shell-as-default)