### setup FTP server in linux rocky
1. install **vsftpd**
  ```bash
      sudo dnf install vsftpd -y
  ```
2. open services and make it run when system boot
  ```bash
      sudo systemctl enable --now vsftpd
  ```

3. check services status
  ```bash
      sudo systemctl status vsftpd
  ```