# SSH

## ssh-keygen

- C:\Windows\System32\OpenSSH\ssh-keygen
- Generate private key và public key
    ```
    ssh-keygen -f C:/Users/<localuser>/.ssh/key/<host_name>_rsa
    ```
- Output file gen ra bao gồm 2 file
    ```
    host_name_rsa       (private key)
    host_name_rsa.pub   (public key)
    ```

## Remote - SSH vscode

![Remote - SSH logo](remote-ssh.png "Remote - SSH")

- Configure thông tin về SSH server thông qua file config
    ```
    F1 > Remote-SSH: Open remote configure file > C:/Users/<localuser>/.ssh/config
    ```
    ![Open-ssh-config](Open-ssh-config.png "Open-ssh-config")

    Add
    ```
    Host <host_name>
    HostName <host_name>
    User <remoteuser>
    Port 22
    PreferredAuthentications publickey
    IdentityFile "C:/Users/<localuser>/.ssh/<host_name>_rsa"
    ```
- Copy public key (`host_name_rsa.pub`) đã gen từ local machine sang server machine và đổi tên thành `authorized_keys`
    ```
     <remoteuserhome>/.ssh/authorized_keys
    ```
    #### (\*\*) Note about **authorized_keys file**
    - Nếu trên server đã có file này rồi thì chỉ cần copy nội dung của `host_name_rsa.pub` append vào cuối file đó
    - Cần grant quyền cho `authorized_keys` 600
        ```
        chmod 600 <remoteuserhome>/.ssh/authorized_keys
        ```
