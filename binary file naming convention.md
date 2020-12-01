# Conventions used to name binary package files

The names of the binary xPacks follow the following rule:

`xpack-${name}-${semver}-${platform}-${arch}.${ext}`

- name: short lower case, dash separated for multiple words
- semver: includes pre-release as sub-version; 1 or 2 digits; the actual xpack version will add an extra digit
- platform = darwin | linux | win32
- arch = ia32 | x64 | arm | arm64 (ia32 was x32)
- ext = .tar.gz (on darwin and linux) | .zip (on win32)

Changes:

- no more date/time, use semver only
- use node.js platform/arch
- no more 'gnu-mcu-eclipse', use 'xpack'
- .tgz may not be understood in some environments (like Ardono); use explicit .tar.gz
