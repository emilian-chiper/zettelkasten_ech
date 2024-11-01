### Meta
2024-10-24 13:11
**Tags:** [[c]] [[c_getting_started]]
**Status:** #completed 

### Compilers
Different compilers implement different versions of the C Standard.

Many compilers for embedded systems support only C89/C90.

Popular compilers for Linux and Windows work hard to support modern versions of the C Standard, up to and including support for C2x.

#### GNU Compiler Collection
The *GNU Compiler Collection (GCC)* includes frontends for C, C++, and Objective-C, as well as other languages.

GCC has been adopted as the standard compiler for Linux systems, although also available for Windows, macOS, and other platforms.

```BASH title:script.sh
sudo apt-get install gcc
gcc --version
```

#### Clang
```BASH title:script.sh
sudo apt-get install clang
clang --version
```