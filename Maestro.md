**IMPORTANT** must be on ADSL network

## To connect using serial:
```bash
ssh root@192.168.0.191
```
Username: root
Password: admin
```bash
minicom -D /dev/ttyUSB0
```

## To connect using ssh:
```bash
ssh root@192.168.0.146
```
Username: root
Password: admin

## Lom
### Lom Using WEB insterface:
https://192.168.1.49/#login
Username: sysadmin
Password: superuser

### Enter Using Serial And SSH
1. open ssh to device
2. opem serial to device
3. run this command on ssh
   ```bash
   Console_LOM_Host.sh lom 
   ```
4. change the baudrate to 38400 (using minicom ctrl + A , P and then D)
5. now can use lom using the serial connection

### Exit lom using serial and ssh
1. run this command on ssh
   ```bash
   Console_LOM_Host.sh host
   ```
2. 
## IPPOWER:
**relay 1**
Link to website: http://192.168.0.215:5000/

## Working with maestro
### Start
```
rdim start
```

### Commands
```
Usage: rdimctl <command> [parameters]
   Commands List:
rdimctl get_dev_num - get total number of rdi devices.
rdimctl get_port_link <port> - get link status 
rdimctl get_port_list        - get port list 
rdimctl get_temp             - read internal Temperature Sensor
rdimctl sfp_read <port num> <offset> <page> <len>
rdimctl get_sfp_info <port num>
rdimctl get_sfp_diag <port num>
```

### Exit
```
rdim stop
```