RTL8188FU driver for Linux kernel 4.15.x ~ 6.5.x (Linux Mint, Ubuntu or Debian Derivatives)

info: rtl8188fu support will be add to rtl8xxxu module of Linux kernel. https://patchwork.kernel.org/project/linux-wireless/patch/b14f299d-3248-98fe-eee1-ba50d2e76c74@gmail.com/


------------------

## How to install

dpkg -i linux-headers-current-arm-64_20.10_arm64.deb

`sudo apt-get install build-essential git dkms linux-headers-$(uname -r)`

`git clone https://github.com/kelebek333/rtl8188fu`

`sudo dkms install ./rtl8188fu`

`sudo cp ./rtl8188fu/firmware/rtl8188fufw.bin /lib/firmware/rtlwifi/`

------------------

## Configuration

#### Disable Power Management

Run following commands for disable power management and plugging/replugging issues.

`sudo mkdir -p /etc/modprobe.d/`

`sudo touch /etc/modprobe.d/rtl8188fu.conf`

`echo "options rtl8188fu rtw_power_mgnt=0 rtw_enusbss=0 rtw_ips_mode=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf`

#### Disable MAC Address Spoofing

Run following commands for disabling MAC Address Spoofing (Note: This is not needed on Ubuntu based distributions. MAC Address Spoofing is already disable on Ubuntu base).

`sudo mkdir -p /etc/NetworkManager/conf.d/`

`sudo touch /etc/NetworkManager/conf.d/disable-random-mac.conf`

`echo -e "[device]\nwifi.scan-rand-mac-address=no" | sudo tee /etc/NetworkManager/conf.d/disable-random-mac.conf`

#### Blacklist (alias) for kernel 5.15 and 5.16 (No needed for kernel 5.17 and up)

If you are using kernel 5.15 and 5.16, you must create a configuration file with following command for preventing to conflict rtl8188fu module with built-in r8188eu module.

`echo 'alias usb:v0BDApF179d*dc*dsc*dp*icFFiscFFipFFin* rtl8188fu' | sudo tee /etc/modprobe.d/r8188eu-blacklist.conf`

#### Blacklist (alias) for kernel 6.2 and up

If you are using kernel 6.2 and up, you must create a configuration file with following command for preventing to conflict rtl8188fu module with built-in rtl8xxxu module.

`echo 'alias usb:v0BDApF179d*dc*dsc*dp*icFFiscFFipFFin* rtl8188fu' | sudo tee /etc/modprobe.d/rtl8xxxu-blacklist.conf`

##### Then you must update initramfs

For initramfs

`sudo update-initramfs -u`

For dracut

`sudo dracut -q --force`

##### Enable rtl8188fu module

Run following command for up to kernel 6.1

`sudo modprobe rtl8188fu`

Run following commands for kernel 6.2 and up

`sudo modprobe -r rtl8188fu`

`sudo modprobe rtl8188fu`

------------------

## How to uninstall

`sudo dkms remove rtl8188fu/1.0 --all`

`sudo rm -f /lib/firmware/rtlwifi/rtl8188fufw.bin`

`sudo rm -f /etc/modprobe.d/rtl8188fu.conf`


------------------

## How to install from PPA repository

You can install rtl8188fu driver with following commands from PPA.

for xUbuntu 16.04-18.04-20.04-22.04-23.04-23.10 / Linux Mint 20.x-21.x

`sudo add-apt-repository ppa:kelebek333/kablosuz`

`sudo apt-get update`

`sudo apt install rtl8188fu-dkms`


You can purge packages with following commands

`sudo apt purge rtl8188fu-dkms`

------------------
