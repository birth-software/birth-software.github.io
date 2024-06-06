---
title: Nativity
---

Nativity is the language and compiler for Birth Software.


# Language draft

## Design decisions and goals

Nativity is aimed to be reliable, fast and secure. It's designed with performance in mind. A few goals:

- Compile at millions of line per second, because hardware allows it and we must take it.
- Have top performance out of the output machine code. For that, we want to offer the programmer as many tools as possible, including manual inline assembly, SIMD and SIMT/SPMD (ispc and shader-like code).
- No garbage collection. If you want it, you write it! Software should be fast and some human conveniences are not worth it to the users or developers.
- One language for everything. Forget about scripting languages, external build systems and all that nonsense.
- Sane cross-compilation.
- Statically-linked binaries when possible.
- Allocation in the standard library is based on virtual memory based arenas.
- 64-bit platform focus
- Types are not values
- Uniforming runtime and comptime evaluation is inherently slow. Specialized solutions must be proposed in order to guarantee efficiency.

## Initial constraints

Before self-hosting, Nativity will only be available on Linux (x86\_64) and MacOS (aarch64). The main reason for this is that these are the platforms commonly used for the lead developer, so extending the target range could be wasteful.

Nonetheless, self-hosting is the main immediate goal of the project, so after that Windows will be supported as well. The supported target range after self-hosted will begin with aarch64 and x86\_64 as cpu architectures and Linux, MacOS and Windows as operating systems. The target range is subject to expansion.

Before self-hosting, there will be no float or vector support. Intrinsics will only be implemented as needed. After self-hosting, an implementation of all this will follow.

## Basic types

### Boolean
Nativity does not support boolean types since there is no hardware concept of it. Instead, integer types should support the boolean use case.

### Integers

Nativity supports 1-bit to 64-bit signed and unsigned integers.

### Float

Nativity does not support float types just yet. Support for 32-bit and 64-bit floats will be added.

### Vector

Nativity does not support vector types just yet. Support will be added.

## Hello, World!

This is a valid hello world with libc linked

```nat {filename="main.nat"}
module std;

fn [cc(.c)] main [export] () s32 {
    std.print("Hello world\n");
    return 0;
}
```

## Conditionals

```nat {filename="main.nat"}
module std;

fn [cc(.c)] main [export] () s32 {
    // With integers:
    >a: u32 = 1;
    if (a) {
        // 'a' is not zero
    } else {
        // 'a' is zero
    }

    // With pointers
    >pointer: ?*u32 = a.&;
    if (?pointer) {
        // Here the variable is shadowed, the attribute "non-null" is added to the backend to the pointer variable
    } else {
        // Here the pointer is null
    }
}
```
