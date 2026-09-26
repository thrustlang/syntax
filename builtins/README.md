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

### Type information

- ``fixedArraySize(Type)`` Returns the element count of a fixed array type, as ``usize``. Example: ``fixedArraySize(array[u8; 4])`` is ``4``.
- ``isSameType(A, B)`` Returns ``true`` when both types are exactly the same.
- ``isPtrLike(Type)`` Returns ``true`` when the type is a pointer or otherwise pointer-like.
- ``isFixedArrayOfSize(Type, N)`` Returns ``true`` when the type is a fixed array of exactly ``N`` elements.

```thrust
if fixedArraySize(array[u8; 4]) != 4 { return 1; }
if isSameType(u32, u32) == false { return 2; }
if isPtrLike(ptr[u32]) == false { return 3; }
if isFixedArrayOfSize(array[u8; 4], 4) == false { return 4; }
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

### Compiler information

- ``compilerVersion()`` Returns the compiler version as a constant string.
- ``debugBuild()`` Returns ``true`` when the compiler is a debug build.

```thrust
if stringLength(compilerVersion()) == 0 { return 1; }
if debugBuild() != false { return 2; }
```

### Strings

- ``stringLength(string)`` Returns the length of a constant string, as ``usize``.

```thrust
if stringLength("hello") != 5 { return 1; }
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
- ``isUnix()``, ``isLinux()``, ``isWindows()``, ``isDarwin()``, ``isApple()``, ``isAix()``, ``isBSD()``, ``isFreeBSD()``, ``isNetBSD()``, ``isOpenBSD()``, ``isAndroid()``, ``isIOS()``, ``isSolaris()``, ``isHaiku()`` Return whether the target runs on that platform or OS family. ``isUnix()`` is true for any Unix-like target (Linux, Darwin/macOS, BSDs, Solaris/Illumos, AIX, Haiku).
- ``is64Bit()``, ``is32Bit()`` Return the pointer width.
- ``isBigEndian()``, ``isLittleEndian()`` Return the endianness.
- ``isX86()``, ``isX8664()``, ``isArm()``, ``isAarch64()``, ``isRiscv64()``, ``isPpc()``, ``isPpc64()``, ``isMips64()``, ``isSystemz()``, ``isLoongarch64()``, ``isWasm()``, ``isWasm32()``, ``isWasm64()`` Return the target architecture.
- ``isElf()``, ``isMachO()``, ``isCoff()`` Return the object file format.
- ``hasPosixThreads()``, ``hasSysvAbi()`` Return platform capabilities.
- ``pointerWidth()``, ``isizeWidth()``, ``usizeWidth()`` Return the width in bits of ``ptr``, ``ssize``, and ``usize``, as ``usize``.
- ``pointerAlign()``, ``maxAlignment()`` Return the alignment in bytes of a pointer and the maximum supported alignment, as ``usize``.
- ``targetCPU()``, ``targetCpuFeatures()`` Return the target CPU name and its enabled features as constant strings.
- ``hasFeature("name")`` Returns whether the target CPU supports the given feature.

These flags are useful with the compile-time conditionals documented in ``statements/compiletime.md``.

## Host information

The machine running the compiler reports information through these builtins:

- ``hostOsName()``, ``hostArch()``, ``hostEndian()`` Return the host operating system, architecture, and endianness as constant strings.
- ``currentTimestamp()`` Returns the current timestamp, as ``usize``.
- ``processorCount()`` Returns the number of host processors visible to the compiler, as ``usize``.
- ``pageSize()`` Returns the host memory page size, as ``usize``.
- ``cpuCacheLineSize()`` Returns the host CPU cache line size, as ``usize``.
- ``hostName()`` Returns the host name as a constant string.

## Token builtins

These names are reserved words. The compiler translates them directly to LLVM operations.

- ``halloc(Type)`` Allocates memory on the heap for a value of the given type. Returns ``ptr[Type]``.

```thrust
var p: ptr[u32] = halloc(u32);
```

- ``memcpy(src, dst, size)`` Copies a memory block from ``src`` into ``dst``. Returns ``ptr``.
- ``memmove(src, dst, size)`` Moves a memory block from ``src`` into ``dst``. Returns ``ptr``.
- ``memset(dst, value, size)`` Fills a memory block with a byte value. Returns ``ptr``.

```thrust
var a: ptr[u32] = halloc(u32);
var b: ptr[u32] = halloc(u32);

memcpy(a as ptr, b as ptr, sizeOf(u32));
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

- ``CString`` is a builtin alias for ``array[char]``. String literals are constant string values; use ``const array[char]`` when the value must be viewed as immutable.

Normal string literals, written ``"text"``, are null-terminated. Non-null-terminated string literals are written ``n#"text"``.

> [!NOTE]
> ``isSameType(A, B)`` compares types after removing ``const`` wrappers, so it checks practical type equivalence rather than strict spelling identity.
