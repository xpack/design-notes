# Conventions used to name binary package files

The current names from GNU MCU Eclipse will change to:

`xpack-${name}-${semver}-${platform}-${arch}.${ext}`

- name: short lower case
- semver: includes pre-release as sub-version; 1 or 2 digits; the actual xpack version will add an extra digit
- platform = darwin | linux | win32
- arch = x32 | x64 | arm | arm64
- ext = .tar.gz (on darwin and linux) | .zip (on win32)

Changes:

- no more date/time, use semver only
- use node.js platform/arch
- no more 'gnu-mcu-eclipse', use 'xpack'
- .tgz may not be understood in some environments (like Ardono); use explicit .tar.gz
