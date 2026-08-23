<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Imports and Modules

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``import`` statement brings code from another file into the current one. A module can export functions, statics, constants, structs, enums, and type aliases.

## File imports

A file is imported by its path, written as a string literal. The path is relative to the current file.

```thrust
import "other.thrust";
```

Symbols from the imported module are reached with the ``::`` operator, using the module name. Without an alias, the module name comes from the file name.

```thrust
import "other.thrust";

fn main() s32 @public {
    return other::answer();
}
```

## Aliases

The ``as`` keyword gives the module another name. The alias can be a path with several parts.

```thrust
import "other.thrust" as dep;
import "vector.thrust" as simd::vec;
```

```thrust
var x: simd::vec::U8Int = simd::vec::pepito as u8;
```

## Selective imports

The ``only`` keyword brings in just the listed symbols.

```thrust
import "other.thrust" only { stack, counter };
```

## Qualified module paths

Modules can be imported with their qualified path, and symbols are reached the same way.

```thrust
import module_a::sub::module_b;

var value: module_a::sub::module_b::MyType = 0;
```

## Re-exports

A module that imports another one can pass its symbols along. When ``b.thrust`` imports ``c.thrust`` as ``inner`` and exposes a ``depth`` value, a file that imports ``b.thrust`` can read ``inner::Depth`` through it.

```thrust
// c.thrust
type Depth @public = u16;

// b.thrust
import "c.thrust" as inner;

static mut depth: inner::Depth @public @extern("depth") = 3;

// a.thrust
import "b.thrust" as dep;

fn main() s32 @public {
    return dep::depth as s32;
}
```

## C imports

The ``importC`` statement imports an entire C library at once.

> [!WARNING]
> ``importC`` is **unstable**. It only works when the compiler runs in unstable mode, and it can change or disappear.

```thrust
importC "mylib";
```

Import and module syntax is **stable**, except ``importC`` which is **unstable**.