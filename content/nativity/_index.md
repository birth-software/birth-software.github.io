---
title: Nativity
next: first-page
---

Nativity is the language and compiler for Birth Software.

## Hello, World!

```nat {filename="main.nat"}
const std = #import("std");

const main = fn () *!void {
    std.print("Hello world\n");
}
```
