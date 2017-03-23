Basic connect:

http://www.stevencombs.com/chip/2016/08/07/mac-to-chip-serial-connection.html

##WANT
To cross compile open frameworks and copy them to networked devices.

###RP3
Similar links that show process for a *shared* .img from a vagrant box to a networked device.
You compile oF programs in vagrant and then ssh them over. You can have clusters of Pi's.

https://github.com/twobitcircus/rpi-build-and-boot

https://holisticsecurity.io/2016/04/12/provisioning-massively-crosscompiled-bin-rpi-armv7-using-vagrant-virtualbox-ansible-python/

###CHIP
The cross compiling could work with a Chip. Instead of using the raspian jessie .img in vagrant you could use the debian jessie 8.7 iso detailed here:

https://github.com/dotzero/vagrant-debian-jessie

##
oF install

https://github.com/zealtv/ofInstallChip
