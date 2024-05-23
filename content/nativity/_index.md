---
title: Nativity
next: first-page
---

Nativity is the language and compiler for Birth Software.

## Hello, World!

This is a valid hello world with libc linked

```nat {filename="main.nat"}
module std;

fn [cc(.c)] main [export] () s32 {
    std.print("Hello world\n");
    return 0;
}
```
