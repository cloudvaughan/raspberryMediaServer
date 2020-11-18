# Setup of Raspberry Pi
Useful Links:
1. Enable Headless Remote Access [Instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) 

Basic: Enable SSH on a headless Raspberry Pi (add file to SD card on another machine) 
Place an empty File on root, file name ssh 

2. Setup Wifi Headless [Instructions](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
3. Default User Raspberry Pi [Instructions](https://www.raspberrypi.org/documentation/raspbian/updating.md)
 
Steps 

- Install OS onto SD 
- Add ssh file, enables headless ssh
- Change configuration using sudo raspi-config
	- Update Localization Settings
	- Extend memory
- Update the raspberry pi
	-`sudo apt update`
	- `sudo apt full-upgrade` 
- Mount HDD 
	- `sudo apt install ntfs-3g`
	- `sudo reboot` 
	- Create the drive mount location `sudo mkdir /mnt/(driveName)
	- Get list of drives `sudo blkid`
	- Mount Drive: `sudo mount /dev/sda1 /mnt/(driveName)` 
- Mount Drive on Boot Up
	- `sudo nano /etc/fstab`
	- add following line:
		`UUID=6E0C10360C0FF83B  /mnt/(driveName) ntfs defaults,auto,users,rw,nofail 0 0` 

