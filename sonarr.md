# Installing Sonarr

We will be installing on Raspbian 10(Buster), OS installed as per [Setup](setupRasp.md)


- Follow the Instructions on Sonarr Downloads
	- [Link](https://sonarr.tv/#downloads-v3-linux)
- You will need to do the optional installations 
- Install mono
	- Follow instructions 
	- [Link](https://www.mono-project.com/download/stable/#download-lin-raspbian)
	- This takes a bit of time
- Install MediaInfo repository
	- [Link](https://mediaarea.net/en/Repos#deb)
	- Follow commands for deb based distributions
	

## Installation Steps
1. Install the optionals, mono and MediaInfo

Add Mono Repository
```
sudo apt install apt-transport-https dirmngr gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://download.mono-project.com/repo/debian stable-raspbianbuster main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
```
Install Mono
```
sudo apt install mono-devel
```
Test Installation

Follow Instructions on [this page](https://www.mono-project.com/docs/getting-started/mono-basics/)

2. Add Sonarr Repository
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb https://apt.sonarr.tv/debian buster main" | sudo tee /etc/apt/sources.list.d/sonarr.list
sudo apt update
```
3. Install Sonarr
```
sudo apt install sonarr
```
4. View Sonarr

Browse to http://localhost:8989 to start using Sonarr.
(Replace 'localhost' with your server IP if you're connecting remotely)
