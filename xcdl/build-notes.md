# Build Notes

## Build configurations

A build configuration is a collection of definitions that
produce one or more artefacts that share some
common properties, for example debug/release for a given platform
and a given set of tools.

Usually the artefacts are application binaries or test binaries.

A project may define multiple build configurations and
xpm is able to manage them.

## Components

A component is a collection of source files that are build using the same
configurations.

Components are organised in hierarchies.

Components can define multiple configuration properties that
translate into build options (like preprocessor definitions, compile
options, etc).

Components are stored in projects, one project being able to
store multiple components.

Components can be contributed to the build in several ways:

1 - as a collection of source files with their compile options (for 
example for header only C++ libraries)
2 - as a collection of already compiled object files
3 - as a static library
4 - as a shared library

## Transparent/forward (no artefacts)

This is more or less similar to CMake INTERFACE libraries.

The target does not produce any artefacts, it basically passes all
dependencies to its parent(s).

The lists of source files, include folders, compile options are concatenated
and forwarded to the parent.

## Artefacts

This target collects all dependencies and builds the artefacts (for example
it compiles the source files).

It passes the created artefacts and the public dependencies to its parent(s).

For these targets it is useful to define separate public and private
sets of options. They are both applied when building the current
targets, but only the public ones are passed up to the parents.

## Multiple faces

A component can define multiple targets, for example transparent and objects.

---

## Historical context

### make in-source builds

The first notable Unix build tool was `make`. It was able to automate
in-source builds, i.e. builds performed in the same folder as
the source files.

### debug/release out-of-tree builds

As tools progressed, it became common practice to use separate debug
and release configurations.

For this to be possible, the builds had to be performed in separate
folders, distinct from the source folders.

Several tools at that time supported this; a notable example was
**Eclipse CDT**, which created separate Debug/Release build folders,
populated with make fragments referring to the source folders.

The compile options were defined for the entire project and applied to
all source files, per each configuration. For special cases, it was
possible to define custom options for individual files or folders, or
to split the project into library projects, referenced by the main
project.

### autotools

As the complexity of the projects grew, and the need to adapt the
builds to run on different platforms became a necessity, various
tools to generate the make files were created.

One of the early ones was the **autotools** (autoconf, automake),
that used the M4 macro language to define templates, instantiated
for each specific use case.

It supported out-of-tree builds and generated complex makefiles.

### pkg-config

`pkg-config` was created to provide the necessary details for compiling
and linking a program to a library.

Each library is expected to provide a configuration file where
the compile and link options required when compiling and linking the
application with the library.

The `pkg-config` executable can be used by autotools to extract
these options from the file in order to add them to the build.

### CMake

A different path took **CMake**, which introduced a list-based language
to define complex build configurations.

With time, it evolved into a mature tool, able to build any project,
with multiple artefacts of any type.

However, the language itself is not exactly easy to use, and requires
a steep learning curve.

### meson

As a reaction to CMake's lax but arcane syntax, meson came with a very
strict language. It can probably run builds for most projects, but the
strict restrictions (like no functions or macros, immutable objects)
make things very difficult in some situations.

## Build strategies

### Monolithical builds

Since Eclipse CDT was a reference tool many years, its monolithical
builds became the norm, especially in embedded projects.

As mentioned before, in this scenario all compile options are defined
at the top project level and all source files are compiled with the
same commands. (Custom options could be applied to files or folders,
but this is not relevant at this point.)

Monolithic builds are fine for regular applications, but might be
inefficient when building tests, since the same sources must
be compiled repeatedly for each test executable.

Monolithic builds are supported by CMake via INTERFACE libraries,
and by meson via regular dependencies.

### Modular builds

Modular projects are defined as separate libraries, with clear dependency
chains.

Each library can be built separately, with its own specific compile
options.

This is an advantage when building multiple tests, since the library can be
built only once and linked to each test.

Libraries are usually `.a` files, and static libraries use names starting
with `lib`. (Dynamic libraries are not used in embedded applications).

Static libraries cannot be used if they define or use weak symbols,
since current linkers are not able to resolve them from libraries.

To avoid this, CMake provides a special type of library, the OBJECT library,
that builds the object files and propagates them as a collection to the
parent, without packing them as an archive, thus avoiding the linker
limitation.

### Common compile options

For cross builds it is necessary to define the target device or
architecture, and possibly other options.

These definitions must be consistent across all sources that are part of
an artefact, and are generally defined at the executable artefact level,
being propagated down to all dependencies.

### Common compile options groups

Assuming a dependency chain of libraries, with the top as the desired
artefact, usually an executable (the application or a test),
each has a collection of dependencies and may appear as a dependency
to one or more other artefacts.

If multiple artefacts use the same common compile options, they can
all use the same build of a library, otherwise the common compile options
must be grouped and for each group there must be a separate build folder
of all chained libraries.

### Public vs private options

Each library can define separate options for compiling its own
sources and for passing them to its parent artefacts.

These include:

- header folders
- preprocessor definitions
- compile options

The general rule is that the regular definitions are public, i.e. are
applied both to the local sources and propagated up to the parent artefacts.

If necessary, separate private definitions can be defined, that will not be
propagated to the parent artefacts.
