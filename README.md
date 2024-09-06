# Arch Linux on WSL 2
Basic instructions on installing Arch Linux for WSL 2.  
> Based on [Import any Linux distribution to use with WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro)


## 0 Prerequisites
- Several Windows features in control panel turned on
  - Windows Subsystem for Linux
  - Virtual Machine Platform
- A running Linux distro
  - in WSL 2
  - with Docker installed
    - quick installation: `curl -fsSL https://get.docker.com -o get-docker.sh`, then `sudo sh get-docker.sh`

## 1 Obtain the tar file via Docker
1. Start the distro.
2. Switch to root (for not typing too many `sudo`s).
```bash
su root
```
3. Start Docker service.
```bash
service docker start    # non-systemd, e.g. init.d
```
```bash
systemctl start docker  # systemd
```
4. Pull Arch image.
```bash
docker pull archlinux
```
5. Create a container.
```bash
docker run archlinux
```
6. Get container ID.
```bash
DockerContainerID=$(docker container ls -a | grep -i archlinux | awk '{print $1}')
```
7. Export into tar.
```bash
docker export $DockerContainerID > /mnt/d/archlinux.tar
```
## 2 Importing the tar file into WSL
1. Start a shell.
2. Execute `wsl --import <DistroName> <InstallLocation> <InstallTarFile>`.
```PowerShell
wsl --import Arch D:\arch-wsl2\ D:\archlinux.tar
```
3. Check it out.
```Powershell
wsl -l -v
```
4. Start and configure.
```bash
wsl -d Arch
```
