# Updating the Linux OS
Updating the system is the most basic hardening step you can take. This will prevent your system from being vulnerable from security flaws that have been patched. 

Updating consists of two steps.
1. Updating the Linux OS repositories   
   `sudo apt update`
2. Applying the updates to your system  
   `sudo apt upgrade -y`  
    This step takes a very long time and the -y flag is to avoid having to type yes to apply the updates manually.

# Updating the Raspberry PI Firmware

Recall that firmware is the code needed to run the hardware specifically. Losing power or interupting the progress during this operation could brick the Pi, so some care should be taken when doing this.

`sudo rpi-update`

## Updating to the latest Raspbian OS version

1. Switch the system to pull from the newer OS repositories.  
   `sudo nano /etc/apt/sources.list`  
   scroll down until you get a line that looks like this:  
   `deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi`  
   then replace 'stretch' with 'buster' (or whatever two OS versions are applicable in your case).  Make sure to save the changes to the file with `ctrl-X`.
2. Update the new OS repositories  
   `sudo apt-get remove apt-listchanges`

3. Apply the upgraded OS repositories to your system  
   `sudo apt dist-upgrade`

4. Remove the old OS repositories  
   `sudo apt autoremove -y`

5. Tidy up softeware dependencies  
`sudo apt autoclean`

6. Reboot the system  
   `sudo reboot`

## Updating to Raspberry OS version  
This can only be done from buster version Raspbian but is very similar to the process above.

`sudo apt update`  
`sudo apt dist-upgrade -y`  
`sudo rpi-update`  
`sudo nano /etc/apt/sources.list`  
    change   
    `deb http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi`   
    to   
    `deb http://raspbian.raspberrypi.org/raspbian/ bullseye main contrib non-free rpi`  
`sudo apt update`  
`sudo apt dist-upgrade`  
`sudo apt autoclean`  
`sudo reboot`  