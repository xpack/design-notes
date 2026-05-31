# Naming CDL variables

## Top presence definitions

These definitions are generated for all packages

### XXX_INCLUDES_YYY

To help components adjust to the presence or absence of some packages, and
to minimise the dependencies, the xCDL Framework can generate a
separate file (like `generated/xcdl-active.h`) with definitions for each 
active package included in the current xCDL configuration.

## Capabilities definitions

### XXX_HAS_YYY

These definitions can be used by platform/device/architecture packages
to represent various capabilities, usually hardware related, like the
presence of peripherals or features.

## Definitions without values

Should be checked with `#if defined(XXX_...)` or `#ifdef XXX_...`.

### XXX_USE_YYY

Examples:

- `MICRO_OS_PLUS_USE_TRACE_SEMIHOSTING_STDOUT`

### XXX_DEBUG, XXX_DEBUG_YYY

Examples:

- `MICRO_OS_PLUS_DEBUG` - special case, enable overall debug;
  passed on the command line
- `MICRO_OS_PLUS_DEBUG_SYSCALLS_BRK`

### XXX_TRACE, XXX_TRACE_YYY

Enable tracing individual cases.

Examples:

- `MICRO_OS_PLUS_TRACE` - special case, enable overall trace;
  passed on the command line
- `MICRO_OS_PLUS_TRACE_UTILS_LISTS`
- `MICRO_OS_PLUS_TRACE_UTILS_LISTS_CONSTRUCTORS`

## Definitions with values

Should be used in expressions of the corresponding type.

### XXX_INTEGER_YYY

Examples:

- `MICRO_OS_PLUS_INTEGER_TRACE_PRINTF_BUFFER_ARRAY_SIZE (42)`
- `MICRO_OS_PLUS_INTEGER_SEMIHOSTING_MAX_OPEN_FILES (42)`

### XXX_BOOL_YYY

Examples:

- `MICRO_OS_PLUS_BOOL_STARTUP_GUARD_CHECKS (true)`

### XXX_STRING_YYY

Examples:

- TBD

## Definitions of types

### XXX_TYPE_YYY

The values are special and represent expressions that can be used
as types to define variables or other types.

Examples:

- TBD

## Links

- <http://micro-os-plus.github.io/reference/cmsis-plus/group__cmsis-plus-app-config.html>
- <https://doc.ecoscentric.com/cdl-guide/language.html#language.naming>
