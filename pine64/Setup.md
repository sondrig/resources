General instructions can be found in the [pine64 wiki](http://wiki.pine64.org/index.php/Pine_A64_Software_Release#Ubuntu_Linux_Image_.5B20160530.5D_based_on_Longsleep_work.2C_build_by_Pine64), but it lacked some things I found useful to document.

## Perparation (write img to SD card on OSX)

#### Download ubuntu
`wget --show-progress --retry-connrefused http://files.pine64.org/os/ubuntu/xubuntu-xenial-20160502-longsleep-pine64-8GB.zip`

#### Install 7zip
`brew install p7zip`
The zip encryption provided by the PINE4 file means OSX can't normally extract it, but 7zip handles it well and installs easily through [brew](http://brew.sh/).

#### Extract img
`7z e xubuntu-xenial-20160502-longsleep-pine64-8GB.zip`

#### Write image (please take care)
`diskutil list`
Find the disk name, and replace all three "diskn/rdiskn" with the right number before running the commands below.
```
diskutil unmount /dev/diskn
sudo dd if=xubuntu-xenial-20160502-longsleep-pine64-8GB.img of=/dev/rdiskn bs=1m
diskutil unmountDisk /dev/diskn
```
[More info on how to write img to SD card](http://raspberrypi.stackexchange.com/questions/4144/writing-img-file-to-sd-card-from-a-mac)

## Setup

Connect the PINE64 to power & ethernet.
When it's booted, find its IP address (your router's web interface usually shows this, and allows you to make the Pine's IP static).

#### SSH into it
`ssh ubuntu@…`

#### Extend root file system
`sudo resize_rootfs.sh`

#### Update apt-get repository
```
sudo apt-get update
```

#### Install vim
(or another editor [if you find vim difficult](https://www.google.com/search?q=vim+introduction))
`sudo apt-get install vim`

#### Enable passwordless sudo
`sudo vim /etc/sudoers`
Add this line to the end
`ubuntu ALL=(ALL) NOPASSWD:ALL`
Save & exit, sign out, then back in

#### SSH login with key
To enable logging in with key, find your public key. If you're on github you can find it at `github.com/username.keys`, otherwise it's probably on your local computer under the name `.ssh/id_rsa.pub`.
```
mkdir .ssh
vim .ssh/authorized_keys
```
Paste contents of your public key there, save & exit.

This is my local SSH config (found in `.ssh/config`)
```
Host pine
	HostName 192.168.1.74
	User ubuntu
	IdentityFile ~/.ssh/id_rsa.pub
	ForwardAgent yes
```
Which makes it possible to ssh into the pine by just typing:

`ssh pine`

###Cinder
https://github.com/cinder/Cinder/wiki/Cinder-for-Linux-%7C-Ubuntu-15.X-on-x86_64

[Topic on getting it working with OpenGL 2.1](https://forum.libcinder.org/topic/glnext-es-3-angle)

`sudo apt-get install libgles2-mesa-dev`

`mesa-utils-extra`

`libegl1-mesa`

Build cinder with es2 `./cibuild -es2`

