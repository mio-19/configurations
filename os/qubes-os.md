# Usage

Running Linux programs without GPU

## Installation

1. Install Qubes OS 4.1 (btrfs)
1. Clone all templates for backup; create a backup vm; backup sys-*
1. Clone debian template and install apps on the new one

# Templates

## Debian 10

```
sudo sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
# rmdir */

sudo apt install fcitx-googlepinyin aria2 p7zip-full gparted gnome-disk-utility gnome-system-monitor curl python3-pip gimp libreoffice default-jdk maven squashfs-tools vlc 
#texlive-full latexila

sudo sed -i 's/mirrors.ustc.edu.cn/deb.debian.org/g' /etc/apt/sources.list

# building dependencies
#sudo apt install libssl-dev pkg-config libfreetype6-dev fontconfig fontconfig-config
#sudo apt install libfontconfig1-dev libgraphite2-dev libharfbuzz-dev libicu-dev libssl-dev zlib1g-dev

#sudo mkdir /opt/graalvm-ce
#GRAALVM_VERSION=20.2.0
#ALL_PROXY=http://127.0.0.1:8082/ curl -L https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-$GRAALVM_VERSION/graalvm-ce-java11-linux-amd64-$GRAALVM_VERSION.tar.gz | sudo tar --strip-components=1 -xzvC /opt/graalvm-ce
#echo 'export PATH="$PATH:/opt/graalvm-ce/bin"' | sudo tee /etc/profile.d/local-graalvm-ce.sh
#sudo sh -c '. /etc/profile;http_proxy=http://127.0.0.1:8082/ gu install native-image'

#sudo mkdir /opt/maven
#ALL_PROXY=http://127.0.0.1:8082/ curl -L https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz | sudo tar --strip-components=1 -xzvC /opt/maven
#echo 'export PATH="$PATH:/opt/maven/bin"' | sudo tee /etc/profile.d/local-maven.sh

# https://www.jetbrains.com/idea/download/#section=linux
sudo mkdir /opt/idea
IDEA_VER=2020.3.2
ALL_PROXY=http://127.0.0.1:8082/ curl -L https://download.jetbrains.com/idea/ideaIU-$IDEA_VER.tar.gz | sudo tar --strip-components=1 -xzvC /opt/idea

## https://www.jetbrains.com/clion/download/download-thanks.html?platform=linuxl
#sudo mkdir /opt/clion
#ALL_PROXY=http://127.0.0.1:8082/ curl -L https://download-cf.jetbrains.com/cpp/CLion-2020.1.1.tar.gz | sudo tar --strip-components=1 -xzvC /opt/clion

#sudo mkdir /opt/go
#ALL_PROXY=http://127.0.0.1:8082/ curl -L https://dl.google.com/go/go1.14.1.linux-amd64.tar.gz | sudo tar --strip-components=1 -xzvC /opt/go
#echo 'export PATH="$PATH:/opt/go/bin"' | sudo tee /etc/profile.d/local-golang.sh

# # https://visualstudio.microsoft.com/ -> https://code.visualstudio.com/docs/setup/linux
# ALL_PROXY=http://127.0.0.1:8082/ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
# sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
# sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
# # not secure version:
# sudo apt update && sudo apt install code
# ## more secure version: 
# #sudo apt clean && sudo apt-get update && sudo apt-get -d install code
# #dpkg -e /var/cache/apt/archives/code_<TAB>
# #less ./DEBIAN/*
# #rm -fr ./DEBIAN
# #sudo apt-get install code

# There is no such file before
cat << 'EOF' | sudo tee /etc/gtk-3.0/settings.ini
[Settings]
gtk-application-prefer-dark-theme=1
EOF
```

### AppVM

Config Fcitx on the first boot (add googlepinyin and hide status panel and not use system tray icon)

# Upgrade

Fedora
```
sudo dnf upgrade && sudo dnf remove $(dnf repoquery --installonly --latest-limit=-1 -q)
```
Debian
```
sudo apt update && sudo apt full-upgrade && sudo apt autoremove --purge && sudo apt clean
```
Dom0
```
sudo qubes-dom0-update && sudo dnf remove $(dnf repoquery --installonly --latest-limit=-1 -q)
```

# Fix EFI

/boot/efi/EFI/config.sh
```
#!/bin/sh
# https://web.archive.org/web/20210328100018/https://www.qubes-os.org/doc/uefi-troubleshooting/#boot-device-not-recognized-after-installing
rm -fr fedora/ BOOT/
cp -r qubes/. BOOT
cp BOOT/grub.cfg BOOT/BOOTX64.cfg
cp BOOT/grubx64.efi BOOT/BOOTX64.efi
```
