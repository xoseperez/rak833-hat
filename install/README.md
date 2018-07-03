# The Things Network: RAK833-based gateway

Reference setup for [The Things Network](http://thethingsnetwork.org/) gateways based on the RAK833 USB concentrator with a Raspberry Pi host using the RAK833 hat available in this same repository.

> This documentation and installation procedure is based largely on [gonzalocasas](https://github.com/gonzalocasas) and [ttn-zh](https://github.com/ttn-zh) installation procedure for the IMST iC880a with minor changes to make it compatible with the RAK833-hat for the RAK833 module by RAK Wireless.


## Setup based on Raspbian image

- Download [Raspbian Jessie Lite](https://www.raspberrypi.org/downloads/)
- Follow the [installation instruction](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to create the SD card
- Plug the RAK833-Hat with the RAK833 module connected
- Start your RPi connected to Ethernet
- From a computer in the same LAN, `ssh` into the RPi using the default hostname:

        local $ ssh pi@raspberrypi.local

- Default password of a plain-vanilla RASPBIAN install for user `pi` is `raspberry`
- Use `raspi-config` utility to configure locale options, expand the filesystem and enable SSH and SPI interfaces:

        $ sudo raspi-config

- Reboot
- Make sure you have an updated installation and install `git`:

        $ sudo apt-get update
        $ sudo apt-get upgrade
        $ sudo apt-get install git

- Create new user for TTN and add it to sudoers

        $ sudo adduser ttn
        $ sudo adduser ttn sudo

- Logout and login as `ttn` and remove the default `pi` user

        $ sudo userdel -rf pi

- Ethernet connection is recommended, if you still want to use WiFi configure the WiFi credentials (check [here for additional details](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))

        $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

        network={
            ssid="The_SSID_of_your_wifi"
            psk="Your_wifi_password"
        }

- Clone [the installer](https://github.com/ttn-zh/RAK833-gateway/) and start the installation

        $ git clone https://github.com/xoseperez/rak833-hat.git
        $ cd ~/rak833-hat/install
        $ sudo ./install.sh

- If you want to use the remote configuration option, please make sure you have created a JSON file named as your gateway EUI (e.g. `B827EBFFFE7B80CD.json`) in the [Gateway Remote Config repository](https://github.com/ttn-zh/gateway-remote-config).
- **Big Success!** You should now have a running gateway in front of you!

# Credits

Credits for [gonzalocasas](https://github.com/gonzalocasas) and [ttn-zh](https://github.com/ttn-zh) for their installation procedure for the IMST iC880a. Also, that procedure is largely based on the awesome work by [Ruud Vlaming](https://github.com/devlaam) on the [Lorank8 installer](https://github.com/Ideetron/Lorank).
