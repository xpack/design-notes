# Library xPacks

The initial design targeted static libraries, useful for embedded and 
portable binaries.

Shared libs are not excluded, but do not seem a priority for now, so they can 
be considered for the design, but implemented later.

commands:

- `xpm run build`
- `xpm run install`

folders in project root:

- `.build`
- `.install`

(if necessary to add variants, use `.build-${variant}`, `.install-${variant}`)

Example of `package.json`:

```json
{
  "xpack": {
    "refs": {
      "lib/libxyz.a": "./.install/lib/libxyz.a",
      "lib/pkgconfig/libxyz.pc": "./.install/lib/pkgconfig/libxyz.pc",
      "include/xyz/xyz.h": "./install/include/xyz/xyz.h"
    }
  }
}
```

When dependencies are satisfied, the references are linked (copied on windows).
(bins can be also processed as references).

The target depends on the project, but most probably is:

- `xpacks/.bin`
- `xpacks/.install`

