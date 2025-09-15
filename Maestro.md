
**important:** must be on ADSL network

## Connect to eboot for serial connection
Using terminal
```bash
ssh root@192.168.0.191
minicom -D /dev/ttyUSB0
```

## ebootPro relay control
In browser: 
[ebootPro manager](http://192.168.0.215:5000/)


## Working with maestro
```
rdim start
```

```
[root@MHO ~]# rdimctl
Usage: rdimctl <command> [parameters]
   Commands List:
get_dev_num - get total number of rdi devices.
get_port_link <port> - get link status 
get_port_list        - get port list 
get_temp             - read internal Temperature Sensor
sfp_read <port num> <offset> <page> <len>
get_sfp_info <port num>
get_sfp_diag <port num>
```