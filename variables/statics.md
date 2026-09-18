<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Statics

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Statics hold a value that lives for the whole program, in a fixed memory location. They are declared at the top level, and can also be declared inside a function body.

```thrust
static counter: u32 = 0;
```

The ``mut`` keyword marks a static as mutable. Without it, the static cannot change after its initialization.

```thrust
static mut counter: u32 = 7;
```

Statics accept attributes, such as ``@public`` to keep the name in the output or ``@extern("name")`` to bind an external symbol.

```thrust
static mut depth: u16 @public @extern("depth") = 3;
```

Top-level statics can also use ``@linkage("kind")`` and ``@align(N)``. An external static must also be public.

Statics accept the same statement modificators as globals and locals where they are meaningful:

- ``volatile`` Forces memory-visible reads and writes.
- ``lazyThread`` Uses lazy thread-local storage.
- ``atomicNone``, ``atomicFree``, ``atomicRelax``, ``atomicGrab``, ``atomicDrop`` Select an atomic ordering.
- ``threadInit``, ``threadDyn``, ``threadExec``, ``threadLDyn`` Select a thread-local storage model.

```thrust
static mut volatile flag: bool = false;
static mut threadInit counter: u32 @public @align(8) = 0;
```

> [!NOTE]
> ``atomicSync`` and ``atomicStrict`` are reserved by the lexer, but they are not currently accepted by the statement-modificator parser.

A static without an initialization keeps whatever the memory holds at load time.

This syntax is **stable**.
