# Arch Linux on WSL 2
Here are some basic instructions for installing Arch Linux on WSL 2 only with wsl.exe.  
Based on [Import any Linux distribution to use with WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro)


## Prerequisites
- WSL & Hyper-V enabled
- A disposable Linux distro running WSL 2 with Docker installed


## Obtaining the tar file via Docker.
1. Start the Linux distro in command line (Debian GNU/Linux 11 in this example).
2. Switch to the root user, since the distro is disposable, to avoid typing too many `sudo`s with Docker commands.
```bash
sudo su
```
2. In bash, start the Docker service.
```bash
service docker start
```
3. Pull the Arch image from the official repository.
```bash
docker pull archlinux
```
4. Create a container using the image.
```bash
docker run archlinux
```
5. Get the container ID.
```bash
DockerContainerID=$(docker container ls -a | grep -i archlinux | awk '{print $1}')
```
6. Export the Arch container into a tar file.
```bash
docker export $DockerContainerID > /mnt/d/archlinux.tar
```
## Importing the tar file into WSL
1. Start PowerShell.
2. In PowerShell, use `wsl --import <DistroName> <InstallLocation> <InstallTarFile>`.
```PowerShell
wsl --import Arch D:\Arch D:\archlinux.tar
```
3. Check it out.
```Powershell
wsl -l -v
```
4. Start Arch and configure.
```bash
wsl -d Arch
```
