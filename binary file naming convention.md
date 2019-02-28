
[2019-03-01]

xpack-${name}-${semver}-${platform}-${arch}.${ext}

platform = darwin | linux | win32
arch = x32 | x64 | arm | arm64
ext = .tgz (on darwin and linux) | .zip (on win32)

semver includes pre-release as sub-version; 1 or 2 digits; 

the actual xpack version will add an extra digit.

changes:

- no more date/time, use semver only
- use node.js platform/arch
- no more 'gnu-mcu-eclipse', use 'xpack'
