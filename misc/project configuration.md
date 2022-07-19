# Project configuration

The project configuration is stored in a JavaScript object that can
be serialized to a JSON object.

It is somehow similar to the CMake cache, but hierarchical.

It is defined at the top project level, but each build configuration
can override any portion of it, so in practice each build configuration
has its own configuration.

Node types are regular JSON types, generally strings.

## Editing

Ideally the configuration should be editable via

- a portable gui tool, like `cmake-gui`
- a ncurses CLI tool, like `kconfig`
- a basic menu based CLI tool

Integration with IDEs might also add nice graphical editors.
