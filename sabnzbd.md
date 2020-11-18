# Installing SABNZBD

We will be installing on Raspbian 10(Buster), OS installed as per [Setup](setupRasp.md)

This was by far the hardest to get right. This installation is going to use the Source Code of sabnzbd, using github

> Don't use the Snap installation. It does not work. As far as I can see it uses a develop branch of the source code and does not function correctly or at all.  

## Pre installation steps
1. Install Python
	Python 3 should be installed as part of the setup process. Check the version
```
python3 --version
```
If Python 3 not installed
```
sudo apt update
sudo apt install python 3
```
2. Installation instructions for Must-have utilities [Link](https://sabnzbd.org/wiki/installation/install-off-modules), we will be installing below.
## Installation Steps
1. Create a directory for the applications
```
sudo mkdir /apps/sabnzbd
cd /apps/sabnzbd
```
2. Clone the github repository
```
git clone https://github.com/sabnzbd/sabnzbd.git
cd sabnzbd
git checkout master
```
3. Install the required python modules
Navigate to the sabnzbd source directory, execute the following code
```
python3 -m pip install -r requirements.txt -U
```
4. Install unrar
Follow the instructions [here](https://gist.github.com/VadimBrodsky/1f567067e2cd438312bb9fd57095a806)
Thanks VadimBrodsky.
You can skip to line 13 as we have already configured the respository
5. Install par2
```
sudo apt install par2 
```
6. Install p7zip-full
```
Sudo apt install p7zip-full 
```
7. Start sabnzbd, this will create the required folders and then stop by pressing ctrl+c
```
python3 /apps/sabnzbd/SABnzbd.py
```
8. Change sabnzbd.ini file to put the ip address for remote access. sabnzbd by default does not allow for remote connection
```
sudo nano /home/(installedUser)/.sabnzbd/sabnzbd.ini
```
Update the following line to the ip address of the raspberry pi.
```
host = 127.0.0.1
```
9. Run sabnzbd in daemon mode.
```
python3 /apps/sabnzbd/SABnzbd.py -d -f "/home/(installedUser)/.sabnzbd/sabnzbd.ini" 
```
10. Complete the configuration as per these instructions in the wizard.
```
Navigate to your ipaddress http://(ipaddress):8080
```
11. Install as a Unix Daemon
This will ensure that sabnzbd runs on startup. More information [here](https://sabnzbd.org/wiki/installation/install-as-a-unix-daemon)
I have modified the script slightly to put a 30 seconds sleep on as this will ensure sabnzbd only runs after network ip address has been configured at boot up.
	1. Create a script to start and stop sabnzbd.
```
sudo mkdir /apps/scripts
sudo nano /apps/scripts/sabnzbd.sh
```
Insert the following updating your details
```
#!/bin/sh
sleep 30
case "$1" in
start)
  echo "Starting SABnzbd."
  /usr/bin/sudo -u pi -H /apps/sabnzbd/SABnzbd.py -d -f /home/(installedUser)/.sabnzbd/sabnzbd.ini
;;
stop)
  echo "Shutting down SABnzbd."
  /usr/bin/wget -q --delete-after "http://(ipaddress):8080/sabnzbd/api?mode=shutdown&amp;apikey=(APIKEY)"
;;
*)
  echo "Usage: $0 {start|stop}"
  exit 1
esac

exit 0

```
	2. Will be using crontab to start the script on boot. Alternatives can be found [here](https://www.dexterindustries.com/howto/run-a-program-on-your-raspberry-pi-at-startup/)
```
cd ~
crontab -e

Add the following code:
@reboot  sh /apps/scripts/sabnzbd.sh start
```
Now to be honest, I am not sure the permissions are configured correct. But it should work.





##Update sabnzbd
```
cd /apps/sabnzbd
git pull
```
