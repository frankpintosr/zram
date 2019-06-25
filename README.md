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
edit /etc/rc.local file to run script on boot
```
sudo nano /etc/rc.local
```
add line before exit 0
```
/usr/bin/zram.sh &
```
Note: If there are existing uncommented entrees in the rc.local file, add & after each one.  My config file has an entry for bluetooth, so I added & after that line. The below example is my rc.local file
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
