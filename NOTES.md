<!-- NOTE FOR  EDITORS OF THIS FILE 
This file is linked to from the EWARM 10.10 release notes regarding "Missing CMSIS headers". 
This should be taken into account when changing the file. 
END OF NOTE -->

## Important Notes

### Missing CMSIS headers
CMSIS, or Cortex Microcontroller Software Interface Standard, consists of a vendor-independent hardware abstraction layer for Arm Cortex processors which provides consistent device support. Developed by Arm, it provides simple software interfaces to the processor and the peripherals, simplifying software re-use, reducing the learning curve for developers, and reducing the time to market for new devices.

Some of the example projects use legacy versions of CMSIS. When building a project requiring them, you might face a fatal error such as:

>Fatal Error[Pe1696]: cannot open source file “core_cm3.h”
## Solution 1
For the latest CMSIS, update the project settings to match your environment.

Clone `CMSIS_6`:
```
git clone https://github.com/ARM-software/CMSIS_6.git
```
Go to **Project Options > C/C++ Compiler > Preprocessor > Additional Include Directories** then add:
```
<path/to/CMSIS_6>/CMSIS/Core/Include
```
Note that some registers changed from `CMSIS_5` to `CMSIS_6`, so that migrating code might be required in some cases. In such cases, consider [Solution 2](#solution-2).

## Solution 2
Use CMSIS 5 for a seamless experience so that no code migration should be necessary.

Clone `CMSIS_5`:
```
git clone https://github.com/ARM-software/CMSIS_5.git
```
Go to **Project Options > C/C++ Compiler > Preprocessor > Additional Include Directories** then add:
```
<path/to/CMSIS_5>/CMSIS/Core/Include
```

### File names on Linux
Many legacy projects were developed primarily on Windows, where file systems are case-insensitive. As a result, **you may encounter case-sensitivity issues when building these projects on Linux**.

Linux treats file names like `MyFavoriteMCU.icf`, `MYFAVORITEMCU.ICF`, and `myfavoritemcu.icf` as completely different files, whereas Windows sees them as the same. This can lead to broken file references, missing assets, or building errors if the exact case doesn't match.

Adjusting the affected file names to comply with such requirements should fix these issues.

### Path names on Linux
Many legacy projects were developed primarily on Windows, where the path separators can be either backward-slash `\` or forward-slash `/`. Backward-slashes however are not portable across Linux file systems. When building projects on Linux, you might find hardcoded backward-slashes in some path names. Any path names using backward-slashes as separators are going to need to be selectively updated to use forward-slashes wherever required, e.g., on hard-coded include paths.
