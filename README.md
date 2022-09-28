# Arch Linux on WSL 2
Here are some basic instructions for installing Arch Linux on WSL 2 only with wsl.exe.
## Prerequisites
- WSL & Hyper-V enabled.
- A Linux distro running WSL 2 with Docker installed.
## Obtaining the tar file via Docker
1. Start the Linux distro in command line.
2. Commands for example.
```bash
sudo service docker start
docker pull archlinux
docker run archlinux
DockerContainerID=$(docker container ls -a | grep -i archlinux | awk '{print $1}')
docker export $DockerContainerID > /mnt/c/archlinux.tar
```
## Importing the tar file into WSL
1. Start PowerShell.
2. Commands for example.
```PowerShell
wsl --import Arch D:\Arch C:\archlinux.tar
wsl -l -v
wsl -d Arch
```
