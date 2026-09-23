<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Variadic Functions

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

A function marked with ``@arbitraryArgs`` accepts any number of extra arguments. The extra arguments are collected into a variable arguments list (``va_list``) that the body reads with the ``arbitraryArgs`` builtins.

## Declaring a variadic function

```thrust
fn printValues(fmt: CString) s32 @public @arbitraryArgs {
    // ...
}
```

The named parameters are declared as usual; the extra arguments are implicit and not named. Callers can pass any number of them:

```thrust
printValues("%d %d", 1, 2);
```

## The hidden argument count

The compiler prepends a hidden ``usize`` argument with the number of extra arguments passed at each call site. This lets the body know how many arguments it received.

```thrust
fn countArgs(first: s32) s32 @public @arbitraryArgs {
    return arbitraryArgsCount() as s32;
}
```

```thrust
countArgs(0, 1, 2, 3);   // returns 3
```

The hidden count is only added to variadic functions defined in Thrust without ``@extern``. FFI variadic functions (``@extern``) keep the C ABI and do not carry it.

## Reading arguments

- ``arbitraryArgs()`` Returns the current variable arguments list as a ``ptr``.
- ``arbitraryArgFrom(list, T)`` Reads the next argument of type ``T`` from ``list``. Each read advances the list, so the reads must match the order of the passed arguments.
- ``arbitraryArgsCopy(list)`` Copies ``list`` into a fresh list and returns it. Each copy can be read independently.
- ``arbitraryArgsEnd(list)`` Ends a list created with ``arbitraryArgsCopy`` (or ``arbitraryArgsStart``).
- ``arbitraryArgsCount()`` Returns the hidden argument count of the current variadic function.
- ``arbitraryArgsStart()`` Starts a new list for future uses.

```thrust
fn readTwo(first: s32) s32 @public @arbitraryArgs {
    var list: ptr = arbitraryArgs();
    var a: s32 = arbitraryArgFrom(list, s32);
    var b: s32 = arbitraryArgFrom(list, s32);
    return a + b;
}
```

```thrust
readTwo(0, 10, 20);   // returns 30
```

### Supported types

``arbitraryArgFrom`` only accepts scalar and pointer types: integers, floats, pointers, ``bool`` and ``char``. Reading a struct or array type is rejected with ``E0057``; pass a pointer instead.

```thrust
var label: ptr[char] = arbitraryArgFrom(list, ptr[char]);
```

### Reading in a separate function

The reliable ``va_arg`` pattern reads the list from a parameter in another function. The ``collections::vector`` ``forEach`` builds on this:

```thrust
import std::collections::vector;

fn addFactor(value: ptr[s32], args: ptr, count: usize) void {
    var factor: s32 = arbitraryArgFrom(args, s32);
    total = total + value->[0] * factor;
}

var values: vector::Vector[s32] = ...;
vector::forEach(ref values, addFactor, 10 as s32);
```

``forEach`` receives the extra arguments, copies the list on every iteration with ``arbitraryArgsCopy``, and passes the element pointer, the copy, and the hidden count to the callback.

## Opting out with ``@noArgCount``

A variadic function that forwards its list to an FFI variadic — such as the ``vprintf`` family — must not carry the hidden count, because its ABI has to stay C-compatible:

```thrust
fn print(fmt: CString) s32 @public @arbitraryArgs @noArgCount {
    return c::vprintf(fmt, arbitraryArgs());
}
```

Add ``@noArgCount`` to opt out. A variadic function without it carries the hidden count and emits the always-active ``W0033`` warning:

> Variadic function carries a hidden argument count; add @noArgCount if it forwards arbitraryArgs() to an FFI variadic.

Using ``@noArgCount`` on a non-variadic function is an error (``E0013``).

This syntax is **stable**.