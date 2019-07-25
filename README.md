*Note: This was tested on macOS with clang*

Example to show the difference of the binary size depending on compiler flags.

There are three libraries:

* `big`: has a `big()` function, requires `14k`
* `small`: has a `small()` function, requires `816 bytes`
* `bigsmall`: has both functions in the same compilation unit (in the
  same `.cpp` file), requires `14k`, but *depending on which function
  you use*, you should avoid the `big()` cost

There are three executables:

* `usebig`: uses `big()` from `big` library, it should be always a big executable, e.g. `16k`
* `usesmall`: uses `small()` from `small` library, it should be always
  a small executable, e.g. `4.2k`
* `usesmall_with_bigsmall`: uses `small()` from `bigsmall` library, it
  should be a small executable (like `usesmall`, `4.2k`), but
  depending on the compiler options, you will get the cost of `big()`
  function (like `usebig`, `16k`)

With `CMAKE_CXX_FLAGS=""` and `CMAKE_EXE_LINKER_FLAGS=""` we get:
```
usebig                   16K
usesmall                4.2K
usesmall_with_bigsmall   16K
```

With `CMAKE_EXE_LINKER_FLAGS="-dead_strip"` we get:
```
usebig                   16K
usesmall                4.2K
usesmall_with_bigsmall  4.2K
```
