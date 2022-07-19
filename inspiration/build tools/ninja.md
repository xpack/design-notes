# Ninja

https://ninja-build.org/manual.html

Run in the build folder.

Uses `build.ninja`.

An alternate method to clean is `-t clean`; it does not require explicit
rules that list the files, it uses the internal

```
$ ninja -h
usage: ninja [options] [targets...]

if targets are unspecified, builds the 'default' target (see manual).

options:
  --version  print ninja version ("1.8.2")

  -C DIR   change to DIR before doing anything else
  -f FILE  specify input build file [default=build.ninja]

  -j N     run N jobs in parallel [default=10, derived from CPUs available]
  -k N     keep going until N jobs fail [default=1]
  -l N     do not start new jobs if the load average is greater than N
  -n       dry run (don't run commands but act like they succeeded)
  -v       show all command lines while building

  -d MODE  enable debugging (use -d list to list modes)
  -t TOOL  run a subtool (use -t list to list subtools)
    terminates toplevel options; further flags are passed to the tool
  -w FLAG  adjust warnings (use -w list to list warnings)

$ ninja -t list
ninja subtools:
    browse  browse dependency graph in a web browser
     clean  clean built files
  commands  list all commands required to rebuild given targets
      deps  show dependencies stored in the deps log
     graph  output graphviz dot file for targets
     query  show inputs/outputs for a path
   targets  list targets by their rule or depth in the DAG
    compdb  dump JSON compilation database to stdout
 recompact  recompacts ninja-internal data structures

$ ninja -d list
debugging modes:
  stats        print operation counts/timing info
  explain      explain what caused a command to execute
  keepdepfile  don't delete depfiles after they're read by ninja
  keeprsp      don't delete @response files on success
multiple modes can be enabled via -d FOO -d BAR
$ $ ninja -w list
warning flags:
  dupbuild={err,warn}  multiple build lines for one target
  phonycycle={err,warn}  phony build statement references itself

$
```
