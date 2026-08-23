<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Functions

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Functions run code in their own block and context. A function lists its parameters, their types, and a return type.

```thrust
fn my_function(a: u32, b: u32) u32 {
    return a + b;
}
```

A function without a stated return type returns ``void``.

```thrust
fn do_nothing() {}
```

## Prototypes

A function can be declared without a body, ending in ``;``. This is how external and forward declarations are written.

```thrust
fn printf(fmt: const array[char]) s32 @arbitraryArgs @extern("printf") @convention("C");
```

## Named arguments

A call can pass arguments by name. Positional arguments must come first, and named arguments can be reordered.

```thrust
fn sum(a: s32, b: s32) s32 {
    return a + b;
}

fn main() s32 @public {
    var x: s32 = sum(b = 123, a = 10);
    var y: s32 = sum(1, b = 2);
    return x + y;
}
```

## Variadic functions

The ``@arbitraryArgs`` attribute marks a function as variadic. It accepts any number of extra arguments, and reads them with the ``arbitraryArgs()`` and ``arbitraryArg(Type)`` builtins.

```thrust
fn my_printf(fmt: const array[char]) s32 @public @arbitraryArgs {
    return vprintf(fmt, arbitraryArgs());
}
```

Functions are **stable**. Named arguments and variadic functions are part of the stable syntax.