# Install Supervised HomeAssistant in Rpi
Have on mind that installation with Docker container will be without Supervisor(integrations with Grafana etc...) 
For supervised HomeAssistant do the following:(Taken from https://peyanski.com/how-to-install-home-assistant-supervised-official-way/)

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install jq wget curl avahi-daemon udisks2 libglib2.0-bin network-manager dbus apparmor -y
sudo apt --fix-broken install
sudo reboot
```

Install Docker(OPTIONAL PART)
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker pi
docker --version
```

Download packages
```
wget https://github.com/home-assistant/os-agent/releases/download/1.2.2/os-agent_1.2.2_linux_armv7.deb
sudo dpkg -i os-agent_1.2.2_linux_armv7.deb
wget https://github.com/home-assistant/supervised-installer/releases/latest/download/homeassistant-supervised.deb
sudo dpkg -i homeassistant-supervised.deb
```

After this choose raspberry4 in my case(os is 32 bits and not 64 bits, TAKE CARE WITH THIS !!!!!), after that you should login with 192.168.0.69:8123
Run:
```
ifconfig
```
In wlan0 check for the ip , thats the ip of your homeAssistant , the port will be 8123

# Install Unsupervised Homeassistant in Rpi(Docker container)

```
sudo apt-get install docker.io docker-compose
sudo reboot
mkdir ~/home-assistant
nano docker-compose.yml
```
in the docker-compose.yml file write the following:

```
version: '3'
services:
  homeassistant:
    container_name: home-assistant
    image: homeassistant/raspberrypi4-homeassistant:stable
    volumes:
      - /home/pi/homeassistant:/config
    environment:
      - TZ=Europe/Warsaw
    restart: always
    network_mode: host
 ```
 Finally: 
 ```
 sudo docker-compose up -d
 ```
 
# Install HomeAssistant in Your phone

Once HomeAssistant running in the rpi , you will be able to install the app from the playstore in your phone and 
add it as part of your automations. In my case the url will be 192.168.0.17:8123 (command - 'ifconfig' and look for wlan0 ip).
The phone must be in the same WIFI connection as the rpi, so it can detect it automatically
If some problem , go to HomeAssistant app in your android phone and delete all the cache and files and reinstall again
