# Build steps

In general there are multiple steps

- configure (optional)
    - autodiscover tools, libraries, etc
    - application 
- generate
    - content (like headers, expand templates, etc)
    - build files (like makefile, ninja.build)
- build

## Build

The build step is the simplest and, based
on the existing rules, builds the target.

It is the only step executed always with each development cycle.

It runs in the build folder, where previous steps already
prepared the desired build files. It must start the
desired tool (make/ninja/xpninja), according to the selected 
generator.

```
$ cd builddir
$ xpmake build
$ xpmake build all
$ xpmake build clean
```

All full words after build are passed as targets to the builder.

If additional options must be passed to the builder, separator them  
by `--` , otherwise `xpmake` will try to make sense of them
and probably fail.

```
$ xpmake build all -- -j 2
```

Individual tools can be called directly, but this is less portable.

```
$ ninja all
```

## Generate

The generate step must be executed after each change in the project structure,
like adding/moving/removing files, or changes in the build options.

Given the list of source folders, include folders, 
toolchain & tool options, decide what tools to use for each file.

The output is a makefile/build.ninja/xpninja.json file.

It runs in the source tree, and creates the build folder(s):

```
$ cd srcdir
$ xpmake generate --config debug
$ xpmake generate --config debug --config release
```

Optionally it can run in the build folder, pointing to the source folder:

```
$ cd builddir
$ xpmake generate ..
```

If multiple configurations are defined, the invocation should name one:

```
$ cd builddir
$ xpmake generate --config debug ..
```

Note: the initial name was `xmake`, but it colided with the lua make tool;
`xbld` might need some reconsideration.
`xgen`, `xgbl`, `xpre`, `xpb`, `xbg`.

Possibly allow for CMake/meson to be used in this step too.


## Configure

This step is not very well defined for now.

It should do something similar to eCos CDL, i.e. decide which
files enter the build, and which options to be used for the build.

A second purpose is to generate headers or other files based on templates.

In CMake style builds, it should discover the toolchain and the system
characteristics.

Probably it should also support the functionality of CMake cache variables.

The original tool name was `xcdl`; the current proposal is `xpcdl`; other names: `xcf`, `xcfg`.


## Integration

Q: For simple projects, would a single tool that does the generate+build 
be useful?

Q: Should the configure and generate be the same tool? 
