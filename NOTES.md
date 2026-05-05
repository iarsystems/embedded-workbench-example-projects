## Important Notes

### Updated CMSIS headers
CMSIS, or Cortex Microcontroller Software Interface Standard, consists of a vendor-independent hardware abstraction layer for Arm Cortex processors which provides consistent device support. Developed by Arm, it provides simple software interfaces to the processor and the peripherals, simplifying software re-use, reducing the learning curve for developers, and reducing the time to market for new devices.

Some of the example projects use legacy versions of CMSIS. When building a project requiring them, you might face a fatal error such as:

>Fatal Error[Pe1696]: cannot open source file “core_cm3.h”

The recommended solution is to use `git` for fetching the required CMSIS headers:
* Linux (as root):
```
cd /opt/iar/
git clone https://github.com/arm-software/cmsis_5
cd ewarm/arm
ln -s ../../cmsis_5/CMSIS
```
* Windows (Administrative Command Prompt):
```
cd /iar/
git clone https://github.com/arm-software/cmsis_5
mklink -d ewarm-10.xx.x ewarm
cd ewarm/arm
mklink -d ../../cmsis_5/CMSIS
```
