# EbootPro

## Update Device Software for Dyingask


## Update Modem Version
### target ver - 25.30.508
#### files needed
1. files/LE910C4-WWX_25.30.508_CUST_057_10_STR.bin.zip
2. files/uxfp_1.14.5-0_source.zip

```bash
systemctl stop ModemManager
uxfp -f LE910C4-WWX_25.30.508_CUST_057_10_STR.bin -p /dev/ttyUSB0
systemctl start ModemManager
mmcli -m any | grep firmware
```
