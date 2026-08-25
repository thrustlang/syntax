<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Primitive Types

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Primitive types are the types built into the language, basic and essential. All types on this page are **stable**.

## Integer types

Unsigned integers:

- ``u8`` unsigned integer, 8 bits.
- ``u16`` unsigned integer, 16 bits.
- ``u32`` unsigned integer, 32 bits.
- ``u64`` unsigned integer, 64 bits.
- ``u128`` unsigned integer, 128 bits.
- ``usize`` unsigned integer, pointer-sized.

Signed integers:

- ``s8`` signed integer, 8 bits.
- ``s16`` signed integer, 16 bits.
- ``s32`` signed integer, 32 bits.
- ``s64`` signed integer, 64 bits.
- ``ssize`` signed integer, pointer-sized.

## Floating-point types

- ``f32`` floating-point, 32 bits (IEEE 754, single precision).
- ``f64`` floating-point, 64 bits (IEEE 754, double precision).
- ``f80`` extended precision floating-point.
- ``f128`` floating-point, 128 bits.
- ``fppc_128`` IBM PowerPC 128-bit floating-point.

## Other scalar types

- ``bool`` Boolean logical type.
- ``char`` A single character, 1 byte.
- ``void`` No value. Used as a return type.

## Constant type

A type wrapped in ``const`` cannot be mutated through that view.

- ``const T`` Constant view of type ``T``.

The null-terminated string type is a constant array of characters: ``const array[char]``. The builtin alias ``CString`` means the same thing.

## Pointer type

- ``ptr`` A pointer without an element type.
- ``ptr[T]`` A strongly typed pointer to ``T``.
- ``ptr[T, N]`` A pointer to ``T`` in the address space ``N``.

Pointers can nest, for example ``ptr[ptr[u8]]``. The ``nullptr`` literal is the null value of any pointer type.

## Array type

- ``array[T]`` An array of ``T`` with a size known at runtime.
- ``array[T; N]`` A fixed array of ``T`` with a size known at compile time.

Arrays can also carry an address space: ``array[T, N]`` and ``array[T; N, N]``.

A fixed array is built with the ``fixed`` literal, which lists the elements inside brackets.

```thrust
var arr: array[s32; 4] = fixed[10, 20, 30, 40];
```

The size of a fixed array can be any expression known at compile time, including arithmetic over constants and builtins.

```thrust
const N: u32 = 8;

static buffer: array[u8; N * 2];
var samples: array[f64; N + 2];
```

## Function type

- ``Fn[param, ...] @attrs -> ret`` A reference to a function that takes the given parameter types and returns ``ret``. The ``@arbitraryArgs`` attribute marks it variadic.

## Example

```thrust
fn main() s32 @public {
    var count: u32 = 1000;
    var balance: f64 = 0.0;
    var done: bool = false;
    var letter: char = 'a';
    var name: const array[char] = "hello";

    var pointer: ptr[u32] = nullptr;
    var values: array[s32; 3] = fixed[1, 2, 3];

    if isFunction(Fn[s32, s32] -> s32) == false { return 1; }
    if isFixedArray(values) == false { return 2; }

    return count;
}
```