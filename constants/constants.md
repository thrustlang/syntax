<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Constants

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Constants hold a single value that cannot change. The value is resolved at compile time, so it can use compile-time builtins such as ``sizeOf``.

```thrust
const U32_SIZE: usize = sizeOf(u32);
const F64_ALIGN: u32 = alignOf(f64);
const TAU: f64 @public = 6.283185307;
```

The ``@public`` attribute keeps the constant name in the output. Top-level constants also accept ``@extern("name")``, ``@linkage("kind")``, and ``@align(N)``. An external constant must also be public. Constants can be declared at the top level and inside a function body; local constants cannot be exported with ``@public``.

Constants can use statement modificators before the name:

- ``volatile`` Forces memory-visible reads.
- ``lazyThread`` Uses lazy thread-local storage.
- ``atomicNone``, ``atomicFree``, ``atomicRelax``, ``atomicGrab``, ``atomicDrop`` Select an atomic ordering.

> [!NOTE]
> ``atomicSync`` and ``atomicStrict`` are reserved by the lexer, but they are not currently accepted by the statement-modificator parser.

```thrust
fn main() s32 @public {
    if U32_SIZE != 4 {
        return 1;
    }
    return 0;
}
```

This syntax is **stable**.
