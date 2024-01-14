# pi-zero-motioneye
Simple instructions on how to install Motioneye on a raspberry pi zero_w <br/> _(should also work on pi zero_w 2)_

##### Most of this can be found on other sites. <br/> This is simply a collection for easier overview. <br/> Most credit goes to https://github.com/motioneye-project/motioneye/

## Requirements

1. Raspberry Pi zero_w or or zero_w 2
2. Fresh installation of Raspbian Buster
(https://pimylifeup.com/download-raspbian/#raspbianbuster)
3. Configured Wifi (ssh is also helpfull)


## Installation
1. Update & Upgrade your raspberry pi

        sudo apt update
   <br>
   
        sudo apt-get full-upgrade

2. Install `ffmpeg` and other `motion` dependencies:

        sudo apt-get install ffmpeg libmariadb3 libpq5 libmicrohttpd12 -y

3. Install `motion`:

        wget https://github.com/Motion-Project/motion/releases/download/release-4.3.2/pi_buster_motion_4.3.2-1_armhf.deb
   <br>
   
        dpkg -i pi_buster_motion_4.3.2-1_armhf.deb

4. Install the dependencies from the repositories:

        apt-get install python-pip python-dev libssl-dev libcurl4-openssl-dev libjpeg-dev libz-dev -y

5. Install `motioneye`, which will automatically pull Python dependencies (`tornado`, `jinja2`, `pillow` and `pycurl`):

        pip install motioneye

    ****note:** If `pillow` installation fails (hangs and ends at 99%), <br>     you can install it from official repos using <br>     `apt-get install python-pil -y` <br>     and rerun <br>      `pip install motioneye`.**

6. Prepare the configuration directory:

        mkdir -p /etc/motioneye
   <br>
   
        cp /usr/local/share/motioneye/extra/motioneye.conf.sample /etc/motioneye/motioneye.conf

7. Prepare the media directory:

        mkdir -p /var/lib/motioneye

8. Add an init script, configure it to run at startup and start the `motionEye` server:

        cp /usr/local/share/motioneye/extra/motioneye.systemd-unit-local /etc/systemd/system/motioneye.service
   <br>
   
        systemctl daemon-reload
   <br>
   
        systemctl enable motioneye
   <br>
   
        systemctl start motioneye

9. To upgrade to the newest version of motionEye, just issue:

        pip install motioneye --upgrade
    <br>
    
        systemctl restart motioneye

## Accessing The Frontend

After having successfully followed the installation instructions, the motionEye server should be running on your system and listening on port 8765. Fire up your favorite web browser and visit the following URL (replacing [your_ip] with... well, your system's IP address):

    http://[your_ip]:8765/

The standard username is `admin` with the password field left empty.

<br>
# Important!
Most of this is just copypasta from: https://github.com/motioneye-project/motioneye/wiki/Install-On-Raspbian#instructions <br> with only a few minor adjustments for an easier overview, etc. <br> -> Again, credit does not go to me at all and I manly just made this to have a simple guide for myself, as most guides are rather old now
