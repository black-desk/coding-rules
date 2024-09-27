# Coding rules

![](https://img.shields.io/github/check-runs/black-desk/coding-rules/master)
![](https://img.shields.io/github/commit-activity/w/black-desk/coding-rules/master)
![](https://img.shields.io/github/contributors/black-desk/coding-rules)
![](https://img.shields.io/github/license/black-desk/coding-rules)

This is a documentation repository recording the coding rules that I
studied and thinking that I should follow in my personal projects.

---------------------------------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in RFC 2119.

## Table of Contents

- [Snippets](#snippets)
- [Documentation](#documentation)
  - [Write the RFC 2119 note near the beginning of
    document](#write-the-rfc-2119-note-near-the-beginning-of-document)
- [Versioning](#versioning)
- [Cpp](#cpp)
  - [Where to install my c/c++ header
    files](#where-to-install-my-cc-header-files)
  - [Note of the pitchfork layout](#note-of-the-pitchfork-layout)
- [Golang](#golang)

## Snippets

This repository provides some code snippets you can found them in the
[UltiSnips](docs/../UltiSnips) and [VSCode](docs/../VSCode) directory.

## Documentation

- [Key words for use in RFCs to Indicate Requirement
  Levels](https://datatracker.ietf.org/doc/html/rfc2119)
- [中文技术文档的写作规范](https://github.com/ruanyf/document-style-guide)

### Write the RFC 2119 note near the beginning of document

RFC 2119 requires that:

> Authors who follow these guidelines should incorporate this phrase
> near the beginning of their document:
>
> The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”,
> “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this
> document are to be interpreted as described in RFC 2119.

Snippets:

``` snippets
snippet RFC_2119 "" b
The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**,
**SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **MAY**, and **OPTIONAL** in this
document are to be interpreted as described in
[RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).
endsnippet

snippet RFC_2119-zh_CN "" b
本文中的关键词**必须**、**禁止**、**必要的**、**应当**、**不应**、**推荐的**、**允许**以及**可选的**的解释见于[RFC 2119][rfc-2119]。

这些关键词与原文中的英语词汇的对应关系如下表所示：

| 中文       | 英语        |
|------------|-------------|
| **必须**   | MUST        |
| **禁止**   | MUST NOT    |
| **必要的** | REQUIRED    |
| **应当**   | SHALL       |
| **不应**   | SHALL NOT   |
| **推荐的** | RECOMMENDED |
| **允许**   | MAY         |
| **可选的** | OPTIONAL    |

[rfc-2119]: https://datatracker.ietf.org/doc/html/rfc2119
endsnippet
```

## Versioning

- [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html)

## Cpp

- [C++ Core
  Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
- [The Pitchfork
  Layout](https://blog.black-desk.cn/pages/pintchfork-layout.html)

### Where to install my c/c++ header files

**DO NOT** directly install header files of your C/C++ project to the
default include directory.

Directly install header files in the default include file search
directories in Unix-like operating system, for examples,
/usr/local/include or /usr/include means that projects building on this
operating system may mistakenly include your header files, especially
for header only library.

For example you have a project vendor the 3.5.0 version of
[nlohmann_json](https://github.com/nlohmann/json) library into the
`<repo>/externals/nlohmann_json`.

To use this library you add `<repo>/externals/nlohmann_json/include` to
include search directories.

Then you use this library as this:

``` cpp
#include "nlohmann/json.hpp"
```

Everything goes well for now, your C++ preprocessor found this file in
`<repo>/externals/nlohmann_json/include/nlohmann/json.hpp`.

But if one day you install a newer version of nlohmann_json into your
system using package manager, and newer header files is installed to
`/usr/include`. Although the `<repo>/externals/nlohmann_json/include`
directory has higher priority when preprocessor looking for headers,
when you writing new code, the IDE or the text editor will list the
header files found in `/usr/include/nlohmann` together with those found
in `<repo>/externals/nlohmann_json/include/nlohmann`.

The newer nlohmann_json adds a header file `json_fwd.hpp`, if you
accidentally include this file into your cpp code, the error message
will says something like the definition of `nlohmann::json` is
ambiguous. It is hard to solve this kind of problems in a large porject
without related experience.

### Note of the pitchfork layout

To follow the pitchfork layout, you should place your source files in
`src` and `include` directory.

So when you writing CMakeLists.txt, you can use these snippets to
quickly list all your source files:

``` snippets
snippet find_cpp_source "" b
`find -regex '\./src/.+\.\(c\|cc\|cpp\|cxx\|h\|hh\|hpp\|hxx\)\(\.in\)?' -type f -printf '%P\n' | sort`
endsnippet

snippet find_cpp_header "" b
`find -regex '\./include/.+\.\(h\|hh\|hpp\|hxx\)\(\.in\)?' -type f -printf '%P\n' | sort`
endsnippet
```

## Golang

- [Standard Go Project
  Layout](https://github.com/golang-standards/project-layout)
