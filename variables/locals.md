<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Locals

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Local variables live in the current scope. They can only be used inside the block where they are declared, and they are gone once that block ends.

A local is declared with ``var``. The full form states the type, the short form infers it from the value, and a declaration without a value leaves it uninitialized.

```thrust
var hello_world: const array[char] = "Hello World!";

var count: u32 = 10;
var other: u32 = count;

var guess := 20;
```

A local can also carry a modificator that changes how the compiler and the hardware treat it:

- ``volatile`` Reads and writes always reach memory, never a cache or a register copy.
- ``lazyThread`` Holds thread-local storage that is created on first use.
- ``atomicNone``, ``atomicFree``, ``atomicRelax``, ``atomicGrab``, ``atomicDrop`` Atomic memory ordering levels.
- ``threadInit``, ``threadDyn``, ``threadExec``, ``threadLDyn`` Thread storage modes.

```thrust
var volatile flag: bool = false;
var atomicRelax balance: f64 = 0.0;
var lazyThread cache: u32 = 0;
var threadInit worker: u32 = 0;
```

The short form still uses the ``:`` token: ``var name := value`` is parsed as a declaration whose type is inferred from ``value``.

Locals can carry attributes before or after the explicit type. The attributes commonly used on locals are ``@heap``, ``@dealloc``, ``@dealloc(function)``, and ``@align(N)``.

```thrust
var buffer @dealloc: ptr[u8] = allocate();
var raw: ptr @dealloc(mem::freeMemory) = mem::allocateMemory(64);
```

> [!NOTE]
> ``atomicSync`` and ``atomicStrict`` are reserved by the lexer, but they are not currently accepted by the statement-modificator parser.

This syntax is **stable**.
