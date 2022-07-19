# Design principles

## Exhaustive discovery vs. installed dependencies

Traditionally, most build systems include a configuration step,
(like running `configure` in autotools projects, or CMake, or meson)
intended to automate the discovery of various
resources, like libraries, tools, files, etc and provide the project
a set of variables that can be later checked to decide if and how
to use these various options.

For example the build system may check if a certain tool is available,
and if the version meets minimum requirements.

The alternative would be to list the tool as a mandatory dependency
and guarantee that a compatible version is installed.

This requires a portable mechanism to install/update tools,
available on common platforms; **xpm** is one such tool.

With such a system, the discovery phase of the configure step is no
longer needed, after an `xpm install` all dependent tools are guaranteed
to be available.
