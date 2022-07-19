# Meson

https://mesonbuild.com/

The syntax of meson is:

```
$ meson [command] [arguments] [options]
```

The setup command takes a builddir and a srcdir argument. If no srcdir 
is given Meson will deduce the srcdir based on pwd and the location of 
`meson.build`.

```
$ meson --help
usage: meson [-h]
             {setup,configure,install,introspect,init,test,wrap,subprojects,help,rewrite}
             ...

optional arguments:
  -h, --help                            show this help message and exit

Commands:
  If no command is specified it defaults to setup command.

  {setup,configure,install,introspect,init,test,wrap,subprojects,help,rewrite}
    setup                               Configure the project
    configure                           Change project options
    install                             Install the project
    introspect                          Introspect project
    init                                Create a new project
    test                                Run tests
    wrap                                Wrap tools
    subprojects                         Manage subprojects
    help                                Print help of a subcommand
    rewrite                             Modify the project definition
$ meson setup --help
usage: meson setup [-h] [--buildtype {plain,debug,debugoptimized,release,minsize,custom}] [--strip]
                   [--unity {on,off,subprojects}] [--prefix PREFIX] [--libdir LIBDIR]
                   [--libexecdir LIBEXECDIR] [--bindir BINDIR] [--sbindir SBINDIR]
                   [--includedir INCLUDEDIR] [--datadir DATADIR] [--mandir MANDIR] [--infodir INFODIR]
                   [--localedir LOCALEDIR] [--sysconfdir SYSCONFDIR] [--localstatedir LOCALSTATEDIR]
                   [--sharedstatedir SHAREDSTATEDIR] [--werror] [--warnlevel {0,1,2,3}]
                   [--layout {mirror,flat}] [--default-library {shared,static,both}]
                   [--backend {ninja,vs,vs2010,vs2015,vs2017,xcode}] [--stdsplit] [--errorlogs]
                   [--install-umask INSTALL_UMASK] [--auto-features {enabled,disabled,auto}]
                   [--optimization {0,g,1,2,3,s}] [--debug]
                   [--wrap-mode {default,nofallback,nodownload,forcefallback}] [-D option]
                   [--cross-file CROSS_FILE] [--native-file NATIVE_FILE] [-v] [--fatal-meson-warnings]
                   [--reconfigure] [--wipe]
                   [builddir] [sourcedir]

positional arguments:
  builddir
  sourcedir

optional arguments:
  -h, --help                                         show this help message and exit
  --buildtype {plain,debug,debugoptimized,release,minsize,custom}
                                                     Build type to use (default: debug).
  --strip                                            Strip targets on install
  --unity {on,off,subprojects}                       Unity build (default: off).
  --prefix PREFIX                                    Installation prefix (default: /usr/local).
  --libdir LIBDIR                                    Library directory (default: lib).
  --libexecdir LIBEXECDIR                            Library executable directory (default: libexec).
  --bindir BINDIR                                    Executable directory (default: bin).
  --sbindir SBINDIR                                  System executable directory (default: sbin).
  --includedir INCLUDEDIR                            Header file directory (default: include).
  --datadir DATADIR                                  Data file directory (default: share).
  --mandir MANDIR                                    Manual page directory (default: share/man).
  --infodir INFODIR                                  Info page directory (default: share/info).
  --localedir LOCALEDIR                              Locale data directory (default: share/locale).
  --sysconfdir SYSCONFDIR                            Sysconf data directory (default: etc).
  --localstatedir LOCALSTATEDIR                      Localstate data directory (default: var).
  --sharedstatedir SHAREDSTATEDIR                    Architecture-independent data directory (default:
                                                     com).
  --werror                                           Treat warnings as errors
  --warnlevel {0,1,2,3}                              Compiler warning level to use (default: 1).
  --layout {mirror,flat}                             Build directory layout (default: mirror).
  --default-library {shared,static,both}             Default library type (default: shared).
  --backend {ninja,vs,vs2010,vs2015,vs2017,xcode}    Backend to use (default: ninja).
  --stdsplit                                         Split stdout and stderr in test logs
  --errorlogs                                        Whether to print the logs from failing tests
  --install-umask INSTALL_UMASK                      Default umask to apply on permissions of installed
                                                     files (default: 022).
  --auto-features {enabled,disabled,auto}            Override value of all 'auto' features (default: auto).
  --optimization {0,g,1,2,3,s}                       Optimization level (default: 0).
  --debug                                            Debug
  --wrap-mode {default,nofallback,nodownload,forcefallback}
                                                     Wrap mode (default: default).
  -D option                                          Set the value of an option, can be used several times
                                                     to set multiple options.
  --cross-file CROSS_FILE                            File describing cross compilation environment.
  --native-file NATIVE_FILE                          File containing overrides for native compilation
                                                     environment.
  -v, --version                                      show program's version number and exit
  --fatal-meson-warnings                             Make all Meson warnings fatal
  --reconfigure                                      Set options and reconfigure the project. Useful when
                                                     new options have been added to the project and the
                                                     default value is not working.
  --wipe                                             Wipe build directory and reconfigure using previous
                                                     command line options. Userful when build directory got
                                                     corrupted, or when rebuilding with a newer version of
                                                     meson.
$
```

The `--buildtype` can be

- plain: no extra build flags are used, even for compiler warnings, 
  useful for distro packagers and other cases where you need to specify 
  all arguments by yourself
- debug: debug info is generated but the result is not optimized, this 
  is the default
- debugoptimized: debug info is generated and the code is optimized 
  (on most compilers this means -g -O2)
- release: full optimization, no debug info

```
$ cd /path/to/source/root
$ CC=clang CXX=clang++ meson setup builddir
```

To run the build:

```
$ ninja -C builddir
```

To run the tests:

```
$ ninja -C builddir test
```

To install (for conventional builds)

```
$ ninja -C builddir install
```
