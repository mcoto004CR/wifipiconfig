# Pi Wifi and SSH Configuration

How to setup wifi, ssh and IP static on Pi

## Enable ssh on Raspberry Pi 4 without any monitor
Well, you can enable ssh on your Pi without any monitor, and it’s not that hard. Let’s get started.

Make the Pi automatically connect to Wi-Fi
You may directly plug an Ethernet cable between your computer and your Pi, so they’re both already in the same network, but let’s say that we’re not going to use an Ethernet cable here.

So, before we can even think of ssh, we first need to make sure the Pi can connect to the Wi-Fi network.

Put your micro SD card back into your computer, and navigate into its root folder (named “boot”).

Here create a file named “wpa_supplicant.conf” (remove any other extension like “.txt”).

Open this file with any text editor (on Windows -> right click + “Open with”), and write the following:

    country=US # replace with your country code
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    network={
        ssid="WIFI_NETWORK_NAME"
        psk="WIFI_PASSWORD"        
    }

Replace WIFI_NETWORK_NAME and WIFI_PASSWORD with the actual name and password of your Wi-Fi network.

Save and quit the file.

If you need to modify the file later this is the location: sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

Great, now the Pi should automatically connect to the Wi-Fi network on boot. But, before you remove the SD card, let’s configure ssh.

## Enable ssh directly on the SD card
Here it’s really simple. Still in the root folder of your SD card (“boot”) create a new file named “ssh”, with no extension.

That’s it! This will enable ssh when you boot the Pi.

Now, remove the micro SD card from your computer, make sure the Pi is powered off, put the SD card into the Pi, and power it on.

Once booted you can ssh on it:

    ssh pi@192.168.xx.xx

## Find your Pi
    
    sudo apt-get install nmap -y
    sudo nmap -sP 192.168.42.1/24

## Change password

    pi@raspberrypi:~ $ passwd
    Changing password for pi.
    Current password: 
    New password: 
    Retype new password: 
    passwd: password updated successfully

## Set static IP

Ge currrent ip
    ifconfig  

    sudo nano /etc/dhcpcd.conf

Enter teh following at the end of the file, note for cable connection use eth0

    interface wlan0
    static ip_address=192.168.XX.XXX/24
    static routers=192.168.1.1
    static domain_name_servers=8.8.8.8

## Update your Pi

    sudo apt update
    sudo apt upgrade
    
