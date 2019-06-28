# zram

Thank you to https://github.com/ric96/zram for the process and original scripts.  I made some changes to the scripts and added some additional instructions.  Follow this process to enable zram at boot and set 1.5GB for the swap file.

Download the script and it will be saved to /usr/bin/zram.sh
```
sudo wget -O /usr/bin/zram.sh https://github.com/frankpintosr/zram.git
```
Make the file executable
```
sudo chmod +x /usr/bin/zram.sh
```
#Backup and download a new rc.local file
```
sudo cp /usr/bin/rc.local /usr/bin/rc.local.backup
sudo wget -O /usr/bin/rc.local https://raw.githubusercontent.com/frankpintosr/zram/master/rc.local
```
Reboot and enjoy
```
sudo reboot now
```
Note: If there are existing uncommented entrees in the rc.local file, add & after each one.  My config file has an entry for bluetooth, so I added & after that line. Your rc.local may not have any additional lines or commands.  The below example is my rc.local file
```
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

/usr/bin/hcitool cmd 0x3F 0x01C 0x01 0x02 0x00 0x01 0x01 &
/usr/bin/zram.sh &
exit 0
```
