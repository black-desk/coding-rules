# Cpp

- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
- [The Pitchfork Layout](https://black-desk.github.io/pages/pintchfork-layout.html)

## Where to install my c/c++ header files

**DO NOT** directly install header files of your C/C++ project to
the default include directory.

Directly install header files in the default include file search directories
in Unix-like operating system,
for examples, /usr/local/include or /usr/include
means that projects building on this operating system may
mistakenly include your header files,
especially for header only library.

For example you have a project vendor the 3.5.0 version of
[nlohmann_json](https://github.com/nlohmann/json) library
into the `<repo>/externals/nlohmann_json`.

To use this library you add `<repo>/externals/nlohmann_json/include`
to include search directories.

Then you use this library as this:

```cpp
#include "nlohmann/json.hpp"
```

Everything goes well for now, your C++ preprocessor found this file in
`<repo>/externals/nlohmann_json/include/nlohmann/json.hpp`.

But if one day you install a newer version of nlohmann_json into your system
using package manager,
and newer header files is installed to `/usr/include`.
Although the `<repo>/externals/nlohmann_json/include` directory
has higher priority when preprocessor looking for headers,
when you writing new code, the IDE or the text editor will
list the header files found in `/usr/include/nlohmann` together with
those found in `<repo>/externals/nlohmann_json/include/nlohmann`.

The newer nlohmann_json adds a header file `json_fwd.hpp`,
if you accidentally include this file into your cpp code,
the error message will says something like
the definition of `nlohmann::json` is ambiguous.
It is hard to solve this kind of problems in a large porject
without related experience.

## Note of the pitchfork layout

To follow the pitchfork layout, you should place your source files
in `src` and `include` directory.

So when you writing CMakeLists.txt,
you can use these snippets to quickly list all your source files:

```snippets {include=../UltiSnips/command/find-cpp-source.snippets}
See ../UltiSnips/command/find-cpp-source.snippets
```
