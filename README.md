# ds2401_3a_200h


Do all commandos on a raspi. I used Raspi 2.

```
apt-get update -y
apt-get upgrade -y

# update the kernel if you want
# rpi-update  

sudo apt-get install bc

sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source
sudo chmod +x /usr/bin/rpi-source
/usr/bin/rpi-source -q --tag-update
rpi-source

git clone git@github.com:Respekt1/ds2401_3a_200h.git && cd ds2401_3a_2000h

# build kernelmodule
make -C /lib/modules/$(uname -r)/build M=$(pwd) modules

sudo insmod w1_ds2413_2100h.ko
dmesg | tail -3
lsmod
```


### connect your 3A_2000h clone chip ...

I used the script from https://github.com/saper-2/rpi-ds2413-2100h.

`wget https://github.com/saper-2/rpi-ds2413-2100h/blob/master/2100h`

make the script file executable
```
chmod +x 2100h

```

### read all one-wire sensors
```
pi@raspberrypi: $ ./2100h s
Small script for testing driver for 1-wire 2100H (clone of DS2413)
Author: saper_2 (Przemyslaw W.)
Version: 0.1 , 2016-04-18 , License: GNU GPL v.XYZ / MPL / CCA :)
 
 
Found 1-Wire devices: 
85-1003c073a2eb


```

### read the 85-XXX sensor
```
pi@raspberrypi: $ ./2100h r 85-1003c073a2eb
Small script for testing driver for 1-wire 2100H (clone of DS2413)
Author: saper_2 (Przemyslaw W.)
Version: 0.1 , 2016-04-18 , License: GNU GPL v.XYZ / MPL / CCA :)
 
 
Reading device 2100H '85-1003c073a2eb' IOs (xxd output):
0000000: 00001111                                               .
   Bits: 76543210
         |||||||+- PIOA Pin state
         ||||||+-- PIOA Out Latch state
         |||||+--- PIOB Pin state
         ||||+---- PIOB Out Latch state
         |||+----- Bit 0 inverted
         ||+------ Bit 1 inverted
         |+------- Bit 2 inverted
         +-------- Bit 3 inverted
```

