---
layout: project
title: Unformat
description: Parsing and extraction of original data from brace style "{}" formatted strings. It basically unformats what you thought was formatted for good.
date: 2017-12-10
links:
  - url: https://github.com/adamyaxley/Unformat
    text: View on GitHub
---

# Background

I've been a huge fan of brace style "{}" string formatting for a long time. Regarding C++, it was only in C++20 that it got official support with the acceptance of [P0645](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p0645r10.html). Even before then there were unofficial libraries that could do the same thing.

However, what I wanted to do was the reverse, to _unformat_ a string and extract data. So I had the idea to write this library that would do exactly that in a simple and elegant way. I make use of constexpr to parse the formatted string, making it incredibly fast (300x faster than std::regex).

# Quick Example
Unformat is simple to use and works on all basic types. See the below example for extracting a `std::string` and an 'int'
```c++
std::string name;
int age;

unformat("Harry is 18 years old.", "{} is {} years old.", name, age);
// name == "Harry" and age == 18
```
As an optimisation, if the format string is known at compile time, it can be parsed into a constant expression by making use of `ay::make_format`. In tests, this increases runtime speed by a factor of 3 or 4.
```c++
std::string name;
int age;

constexpr auto format = ay::make_format("{} is {} years old.");
unformat("Harry is 18 years old.", format, name, age);
// name == "Harry" and age == 18
```

# Speed
Unformat is super awesome back to the future style lightning fast compared to traditional parsing methods. Below is the output from Google Benchmark on unformat_benchmark.cpp. Great Scott!
```
Run on (16 X 2993 MHz CPU s)
03/13/19 18:10:57
--------------------------------------------------------------------
Benchmark                             Time           CPU Iterations
--------------------------------------------------------------------
Unformat                             72 ns         71 ns    8960000
Unformat_ConstChar                   69 ns         70 ns    8960000
Unformat_ConstexprMakeFormat         36 ns         35 ns   19478261
StdStringStream                     844 ns        854 ns     896000
StdRegex                           9975 ns      10010 ns      64000
StdScanf                           1716 ns       1726 ns     407273
```