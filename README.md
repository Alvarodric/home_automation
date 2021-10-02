# Install HomeAssistant in Rpi

```
sudo apt-get update &&
sudo apt-get upgrade -y &&
sudo apt-get install -y python3 python3-dev python3-venv python3-pip libffi-dev libssl-dev libjpeg-dev zlib1g-dev autoconf &&
sudo useradd -rm homeassistant -G dialout,gpio,i2c &&
sudo mkdir /srv/homeassistant &&
sudo chown homeassistant:homeassistant /srv/homeassistant &&
sudo -u homeassistant -H -s &&
cd /srv/homeassistant &&
python3 -m venv /srv/homeassistant &&
source /srv/homeassistant/bin/activate &&
python3 -m pip install wheel &&
pip3 install homeassistant &&
hass
```
