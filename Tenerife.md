load qat if note loaded
lsmod | grep -i qat
cat /sys/bus/pci/devices/0000:01:00.0/sriov_numvfs
cat /sys/bus/pci/devices/0000:05:00.0/sriov_numvfs
lspci | grep -i qat | wc -l
