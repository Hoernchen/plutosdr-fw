# *modified* plutosdr firmware
 This experimental firmware uses a custom library on the host side and a kernel driver on the plutosdr itself (no libiio!)

requires https://github.com/Hoernchen/libosmoplutosdr + http://cgit.osmocom.org/gr-osmosdr/ plutokernel branch

* Build Instructions
 ```bash
 
      git clone --recursive https://github.com/Hoernchen/plutosdr-fw.git
      cd plutosdr-fw
      export CROSS_COMPILE=arm-xilinx-linux-gnueabi-
      export PATH=$PATH:/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin
      export VIVADO_SETTINGS=/opt/Xilinx/Vivado/2016.2/settings64.sh
      make
 
 ```

