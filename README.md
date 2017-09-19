# *modified* plutosdr firmware
 This experimental **rx only** firmware uses a custom library on the host side and a kernel driver on the plutosdr itself (no libiio!)
 
Requires https://github.com/Hoernchen/libosmoplutosdr + http://cgit.osmocom.org/gr-osmosdr/ plutokernel branch

* What

  * RX only
  * Just basic functionality so far - frequency, gain, rate
  
* Why

  * Libiio is the most ~contrived~ generic way for writing strings to sysfs entries i've ever seen.. I don't really want bison and  flex as deps just to control my plutosdr.
  * Libiio is also the most generic way to transfer data from the device to the host - it's probably great as long as it's being used with USB 3.0 which hast plenty bandwidth to spare, which is not the case here. There is nothing generic about the plutosdr, making sure the samples arrive at the host is paramount.
  * Actual usb performance according to the usb transfer timestamps was about 220mbit/s - the kernel driver version maxes out at about 327mbit/s on my machine (Win10)
    * This requires a patched libusb on Windows, because the libusb maintainers couln't agree upon a platform independent way to implement windows specific flags during the past (ten?) years.
    
    
* Build Instructions
 ```bash
 
      git clone --recursive https://github.com/Hoernchen/plutosdr-fw.git
      cd plutosdr-fw
      export CROSS_COMPILE=arm-xilinx-linux-gnueabi-
      export PATH=$PATH:/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin
      export VIVADO_SETTINGS=/opt/Xilinx/Vivado/2016.2/settings64.sh
      make
 
 ```
No need to flash the firmware - just switch your plutosdr to DFU mode
```bash
device_reboot ram
```
then upload the firmware
```bash
dfu-util -D pluto.dfu -a firmware.dfu
dfu-util -e
```
