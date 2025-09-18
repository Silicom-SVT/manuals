# EbootPro

## Update Device Software for Dyingask
### files needed
1. [link](https://silicomltd-my.sharepoint.com/:f:/r/personal/davidr_silicom_co_il/Documents/For_Daniel/Dying_Gasp_image?csf=1&web=1&e=B3LdFA)
### program combined u-boot, kerenl, and rootfs image to emmc;
1. ```echo 0 > /sys/block/mmcblk0boot0/force_ro```
2. ```dd if=/dev/zero of=/dev/mmcblk0boot0```
3. Connect USB modified
4. open CMD in the Windows PC, cd to location with uuu.exe and images
5. ```reboot``` eBoot pro from internal Linux
6. check device is exist ```uuu.exe -lsusb```
7. ```uuu.exe -b emmc_all core-image-base-edge-pro.wic.zst```
8. program u-boot SPL to SPI flash: ```uuu -b qspi imx-boot-edge-pro-emmc.bin-flash_singleboot```
9. ```uuu.exe FB: ucmd reset```

## Update Modem Version
### target ver - 25.30.528
#### files needed
1. files/LE910C4-WWX_25.30.508_CUST_057_10_STR.bin.zip
2. files/uxfp_1.14.5-0_source.zip

```bash
tar -xvzf uxfp-1.14.5-0.tar.gz
date -s "2025-09-01 10:25:00"
./configure
make
make install
cd /home/
```


```bash
systemctl stop ModemManager
uxfp -f LE910C4-WWX_25.30.508_CUST_057_10_STR.bin -p /dev/ttyUSB0
systemctl start ModemManager
mmcli -m any | grep firmware
```

## How to run dying-gask
### file needed
[link](https://silicomltd-my.sharepoint.com/:f:/r/personal/davidr_silicom_co_il/Documents/For_Daniel/Scripts?csf=1&web=1&e=3JVOcc)

# how to run
1. load the dying gasp image and copy the scripts white_leds_test.sh, QMI-ip-setup.sh to /home
2. type
```bash
./white_leds_test.sh &
```
3. type
```bash
cd /home/
mmcli -L
mmcli -m 0
mmcli -m 0 --simple-connect="apn=uinternet"
./QMI-ip-setup.sh
```
4. type
```bash
libgpiod-event
```
5. Switch OFF the main input AC and check that 3 pings were successfully sent
6. Delete the scripts from the unit and load the origonal image

## SystemCTL config
```config
# up and get ip  
[Unit]  
Description=Run udhcpc for ether0  
After=network-pre.target  
Wants=network-pre.target

[Service]  
Type=simple  
ExecStart=/sbin/udhcpc -i ether0  
Restart=on-failure

[Install]  
WantedBy=multi-user.target

#allow from outside  
[Unit]  
Description=Restore iptables rules  
After=network-pre.target udhcpc-ether0.service  
Requires=udhcpc-ether0.service

[Service]  
Type=oneshot  
ExecStartPre=/bin/sleep 30  
ExecStart=/usr/sbin/iptables-restore /etc/iptables/rules.v4  
RemainAfterExit=yes

[Install]  
WantedBy=multi-user.target  

```

```bash
iptables -I INPUT 1 -p icmp --icmp-type echo-request -j ACCEPT  
iptables -I INPUT 1 -m state --state RELATED,ESTABLISHED -j ACCEPT  
iptables -I INPUT 2 -p tcp --dport 22 -j ACCEPT  
iptables-save > /etc/iptables/rules.v4
```
