https://github.com/comakingspace/Seminars/tree/master/Ubuntu_Podman_Homeassistant

# Installing Ubuntu Server

Please download the raspberry pi imager:
https://www.raspberrypi.org/downloads/

Once loaded, please install:
Ubuntu --> Ubuntu Server 20.04.1 LTS (RPi 3/4)

DO NOT Install Ubuntu 20.10 (due to podman not yet being compiled for this)


## Initializing Ubuntu

1. Please put the content of the example user-data file on your SD-Card
2. Please modify the user-data to reflect your desired Username
3. Please put homeassistant.service on your SD card as well
4. Please modify homeassistant.service to reflect your desired username

Generating your SSH Key 
- On Windows: ssh-keygen
- On Linux: ssh-keygen
- On Mac OS: ssh-keygen

Generating a SHA-512 based password hash
- Windows: Use WSL to install Ubuntu….
- Debian based systems: mkpasswd --method=SHA-512
    
    Note: mkpasswd is part of whois: sudo apt install whois
- MacOS: openssl passwd -6
- Others: Try openssl passwd -6

Alternative: Set a plain password and change on first login

## Check installation
```podman --version```


# Install homeassistant
```mkdir .homeassistant```

Try it:

```podman run --label "io.containers.autoupdate=image" -dt --name homeassistant -p 8080:8123 --device /dev/ttyAMA0:/dev/ttyAMA0:rw -v /home/<<<YOUR_USER_NAME>>>/.homeassistant:/config homeassistant/raspberrypi4-homeassistant:stable```


Persist it:
```
sudo mv /boot/firmware/homeassistant.service /etc/systemd/system/homeassistant.service
sudo systemctl daemon-reload
sudo systemctl start homeassistant
sudo systemctl enable homeassistant
```


Now: Connect Visual Studio Code to HomeAsistant
Then: Install HACS


# Further Resources
## Cloud-Init:
- [https://cloudinit.readthedocs.io/en/latest/topics/examples.html]
- [https://help.ubuntu.com/community/CloudInit]

## Podman
- [https://podman.io/getting-started/]
- [https://www.heise.de/developer/artikel/Podman-Linux-Container-einfach-gemacht-Teil-1-4329067.html]
- [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html/managing_containers/finding_running_and_building_containers_with_podman_skopeo_and_buildah]

## Home Assistant
- [https://www.home-assistant.io/docs/]
- [https://hacs.xyz/]
