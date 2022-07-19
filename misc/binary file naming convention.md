# Conventions used to name binary package files

The current names from GNU MCU Eclipse will change to:

`xpack-${name}-${semver}-${platform}-${arch}.${ext}`

- name: short lower case (openocd, arm-none-eabi-gcc, etc)
- semver: includes pre-release as sub-version; 1 or 2 digits; the actual xpack version will add an extra digit
- platform = darwin | linux | win32
- arch = x32 | x64 | arm | arm64
- ext = .tgz (on darwin and linux) | .zip (on win32)

Changes:

- no more date/time, semver only
- use node.js conventions for platform/arch
- 'gnu-mcu-eclipse' replaced by shorter and more generic 'xpack'
