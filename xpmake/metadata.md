# Metadata

Format: JSON

## Versioning

```json
{
  "minimumXpmakeRequired": "0.1.0",
  ...
}
```

## The _option_ object

### Purpose

Define an option, as a single configuration choice.

### Syntax

```json
{
  "options": {
    "name": {
      "description": "...",
      "...": "... other properties ..."
    }
  }
}
```

### Description

The _option_ object is the basic unit of configurability.
Generally each option corresponds to a single user choice.
An option may be a simple yes-or-no choice or it may be something more
complicated such as an array size or a device name.
Options may have associated constraints, so if that option is enabled then
certain conditions have to satisfied elsewhere in the configuration.
Options usually have direct consequences such as preprocessor `#define`
symbols in a configuration header file.

Options are objects with a name and a body. Within a parent node, names
must be unique.

The user choice is expressed during the configuration process and is
reflected in the enabled/disabled statues of the option. For options with
associated values, it is also possible for the user to define a value (if
missing, a default value, either implicit or defined as the property
`defaultValue`, is applied). For these options it is also possible to define
some limits on the possible values that the user can choose.

A separate class of options are the computed options, whose values cannot
be set by the user, but are computed according to a given expression.

### Containers

Options are not containers, so they cannot hold other objects.

### Optional properties

- _parent_: the id of the parent node
- _valueType_: the type of the variable associated with this option
  (none, bool, int, float, string)
- _defaultEnable_: a boolean (expression?) that provides an initial
  value for the option enabled/disabled state
- _defaultValue_: an expression to be used as a default value for this
  option, when the user does not define it explicitly during the
  configuration process
- _generatedDefinition_ - a valid C preprocessor identifier to be
  defined in the header file if the option is active and enabled
- _generatedFile_ - the full path file name of the header where the option
  will generate a definition (if missing, inherited from the parent node)
- _requires_: an array of IDs of other objects to be enabled when this
  option is enabled
- _activeIf_: an array of expressions to be evaluated; if all are true,
  the active state of this option remains true (TODO: work details)
- TODO: add other

### GUI

In a GUI, the _option_ object is a leaf node in a configuration tree, with:

- an icon
- the name
- the description as a tooltip
- a radio button to enable/disable the option (always on for mandatory options)
- (optional) an edit widget to edit the value or a select widget to select
  from a list.

## The _component_ object

### Purpose

Define a component, as a collection of configuration objects.

### Syntax

```json
{
  "components": {
    "name": {
      "description": "...",
      "...": "... other properties ...",
      "options": {},
      "components": {}
    }
  }
}
```

### Description

The _component_ object is a configuration element that can contain
additional options and subcomponents. A _component_ can have the
same properties as an _option_ plus more.

Components are objects with a name and a body. Within a parent node, names
must be unique.

Similarly to _option_ objects, if active and enabled, _component_ objects
can generate preprocessor `#define` lines in a configuration header file,
and decide if a set of source files are included in the build process.

### Containers

Components are containers, so it is possible for a component to include
_component_, _option_, _interface_ objects that
should go below this object in the configuration hierarchy.
These objects can be defined either as embedded children, or can be
read from included files.

### Optional properties

- all those available for _option_
- _compilerSourceFiles_: array of paths to source files
- _compileIncludeFolders_: array of paths to folders with header files
- _compilerDefinitions_: array of preprocessor symbols
- _compilerOptions_: array of compiler options
- _dependencies_: array of IDs to dependencies, usually components that need
  to be built before the current component

Possibly language specific:

- _cCompileIncludeFolders_: array of paths to folders with header files
- _cCompilerDefinitions_: array of preprocessor symbols
- _cCompilerOptions_: array of compiler options
- _cppCompilerIncludeFolders_: array of paths to folders with header files
- _cppCompilerDefinitions_: array of preprocessor symbols
- _cppCompilerOptions_: array of compiler options
