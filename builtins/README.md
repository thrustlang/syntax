<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Builtins

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Built-in functions are part of the compiler and the language. They come in two groups:

- **Compile-time builtins.** They run while the compiler processes the code. They are called with normal call syntax and their result is known at compile time.
- **Token builtins.** They are reserved words that the compiler lowers to LLVM operations directly.

All builtins in this page are **stable**.

## Compile-time builtins

### Type layout

- ``sizeOf(Type)`` Returns the size of a type in bytes, as ``usize``. Example: ``sizeOf(u32)`` is ``4``.
- ``alignOf(Type)`` Returns the memory alignment of a type, as ``u32``.
- ``typeWidth(Type)`` Returns the bit width of a type, as ``usize``.
- ``fieldCount(Type)`` Returns the number of fields of a struct type, as ``usize``.

```thrust
const PAIR_SIZE: usize = sizeOf(pair_u32);
const PAIR_ALIGN: u32 = alignOf(pair_u32);
const PAIR_FIELDS: usize = fieldCount(pair_u32);
```

### Source location

- ``file()`` Returns the current source file as a constant string.
- ``fileLine()`` Returns the current source line, as ``u32``.
- ``currentFuncName()`` Returns the name of the current function as a constant string.

### Compile-time checks

- ``staticAssert(condition, "message")`` Fails the compilation when the condition is not a constant true value.
- ``compileError("message")`` Always fails the compilation with the given message.
- ``compileWarning("message")`` Always reports a warning with the given message.

```thrust
staticAssert(sizeOf(u32) == 4, "u32 must be 4 bytes");
```

### Type predicates

Each predicate takes a type argument and returns a ``bool``:

``isSigned``, ``isUnsigned``, ``isInteger``, ``isFloat``, ``isBool``,
``isChar``, ``isPointer``, ``isArray``, ``isFixedArray``, ``isStruct``,
``isVoid``, ``isConst``, ``isNumeric``, ``isFunction``.

```thrust
if isInteger(u32) == false { return 1; }
if isPointer(ptr[u32]) == false { return 2; }
```

### Target information

The compiler targets a machine described by its target triple. These builtins report about it:

- ``targetOS()``, ``targetArch()``, ``targetVendor()``, ``targetAbi()``, ``targetTriple()`` Return constant strings.
- ``isLinux()``, ``isWindows()``, ``isDarwin()``, ``isApple()``, ``isAix()`` Return whether the target runs on that platform.
- ``is64Bit()``, ``is32Bit()`` Return the pointer width.
- ``isBigEndian()``, ``isLittleEndian()`` Return the endianness.
- ``isX86()``, ``isX8664()``, ``isArm()``, ``isAarch64()``, ``isRiscv64()``, ``isPpc()``, ``isPpc64()``, ``isMips64()``, ``isSystemz()``, ``isLoongarch64()``, ``isWasm()`` Return the target architecture.
- ``isElf()``, ``isMachO()``, ``isCoff()`` Return the object file format.
- ``hasPosixThreads()``, ``hasSysvAbi()`` Return platform capabilities.

These flags are useful with the compile-time conditionals documented in ``statements/compiletime.md``.

## Token builtins

These names are reserved words. The compiler translates them directly to LLVM operations.

- ``halloc(Type)`` Allocates memory on the heap for a value of the given type. Returns ``ptr[Type]``.

```thrust
var p: ptr[u32] = halloc(u32);
```

- ``memcpy(dst, src, size)`` Copies a memory block. Returns ``ptr``.
- ``memmove(dst, src, size)`` Moves a memory block. Returns ``ptr``.
- ``memset(dst, value, size)`` Fills a memory block with a byte value. Returns ``ptr``.

```thrust
var a: ptr[u32] = halloc(u32);
var b: ptr[u32] = halloc(u32);

memcpy(b as ptr, a as ptr, sizeOf(u32));
```

- ``abiSizeOf(Type)`` Returns the size in bytes as the ABI defines it, as ``u64``.
- ``bitSizeOf(Type)`` Returns the size in bits, as ``u64``.
- ``abiAlignOf(Type)`` Returns the alignment as the ABI defines it, as ``u32``.

### Variadic functions

Two builtins support functions with arbitrary arguments:

- ``arbitraryArgs()`` Returns the current variadic argument list, as ``ptr``.
- ``arbitraryArg(Type)`` Reads one variadic argument of the given type.

```thrust
fn print(fmt: const array[char]) s32 @public @arbitraryArgs @extern("printf") @convention("C");
```

## Builtin type

- ``CString`` is a builtin alias for ``array[char]``, the null-terminated string type. You can write ``const array[char]`` or ``CString`` to mean the same thing.