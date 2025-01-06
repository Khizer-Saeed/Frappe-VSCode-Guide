# Guide to connect your WSL With VS Code
**Note the following guide is for connecting your WSL frappe with Visual Studio Code in windows**
## Generate SSH Key in Windows
```bash
ssh-keygen
```
- The above command will generate a .ssh folder in /C/Users/[Your User]/.ssh
- There are going to be 2 files of either name id_rsa and id_rsa.pub (Names Could be different).
- Open .pub file in notepad and copy ssh key

## Create .ssh director and authorized keys file (If not done before)
```bash
cd ~
```
**OR**
```bash
cd /home/[user]
```

```bash
sudo mkdir .ssh
cd .ssh
```

```bash
sudo nano authorized_keys
```
**Paste the ssh in the authorized_keys file**

## Setting Up Port Forwarding

1. Install & Enable SSH Server
```bash
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl status ssh
sudo service ssh reload
```
2. Got to **sshd_config file**
```bash
sudo nano /etc/ssh/sshd_config
```
3. Either Uncomment (Remove # tags) or Write the following options
    - **PubkeyAuthentication yes**
    - **AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2**
    - **PasswordAuthentication no**

4. Reload ssh
```bash
sudo service ssh reload
```

## VS Code Setup
1. Install **Remote Developement Extension** by Microsoft.
2. After it is installed you will be able to see a pc icon (Remote Explorer) on the left bar of VS Code open it.
3. Hover over the SSH section and click on settings icon.
4. Paste the following command in that file:
```bash
Host localhost
  HostName localhost
  User "WSL User Name"
  Port 22
  IdentityFile "Path to your private windows ssh key"
```
