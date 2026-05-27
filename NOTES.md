## Important Notes

### Missing CMSIS headers
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
cd ewarm-10.xx.x/arm
mklink /D ..\..\cmsis_5\CMSIS
```
Replace `ewarm-10.xx.x` by its actual version.

### File names on Linux
Many legacy projects were developed primarily on Windows, where file systems are case-insensitive. As a result, **you may encounter case-sensitivity issues when building these projects on Linux**.

Linux treats file names like `MyFavoriteMCU.icf`, `MYFAVORITEMCU.ICF`, and `myfavoritemcu.icf` as completely different files, whereas Windows sees them as the same. This can lead to broken file references, missing assets, or building errors if the exact case doesn't match.

Adjusting the affected file names to comply with such requirements should fix these issues.

### Path names on Linux
Many legacy projects were developed primarily on Windows, where the path separators can be either backward-slash `\` or forward-slash `/`. Backward-slashes however are not portable across Linux file systems. When building projects on Linux, you might find hardcoded backward-slashes in some path names. Any path names using backward-slashes as separators are going to need to be selectively updated to use forward-slashes wherever required, e.g., on hard-coded include paths.
