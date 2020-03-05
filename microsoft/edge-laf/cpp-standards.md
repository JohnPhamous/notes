# C++ Coding Standards

These are the coding standards from Google for Chromium.

> [Source](https://google.github.io/styleguide/cppguide.html#Namespaces)

- Compile to C++17
- Each header file `.h` needs to have header guards

```cpp
// project/src/path/file.h
#ifndef PROJECT_PATH_FILE_H_
#define PROJECT_PATH_FILE_H_

// Header goes ehre

#endif  // PROJECT_PATH_FILE_H_
```

This prevents the compiler from adding a header file multiple times.

- Don't use `#pragma once`, opt for using `#ifndef`

- Define functions inline only when they are 10 lines or fewer
  - Pro: Inlining a function can generate more efficient object code
  - Con: It can make your object code larger
- Don't use using-directives i.e. `using namespace std`
- Keep variable declarations and initializations close

```cpp
// This is a case where you wouldn't want the declaration and initialization to be together.
for (int i = 0; i < 1000; i++) {
  Foo f; // Calls the constructor and destructor 1000 times, this could be very expensive
  f.DoSomething(i);
}

// Instead we should do this
Foo f; // We only call the constructor and destructor once
for (int i = 0; i < 1000; i++) {
  f.DoSomething(i);
}
```

- Use prefix form for increment/decrement (`--i/++i`) when the value is not needed
  - The prefix form is often more efficient than the suffix form. The suffix form requires an additional copy operation.
