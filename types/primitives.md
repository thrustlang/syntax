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

Pointers can nest, for example ``ptr[ptr[u8]]``.

## Array type

- ``array[T]`` An array of ``T`` with a size known at runtime.
- ``array[T; N]`` A fixed array of ``T`` with a size known at compile time.

Arrays can also carry an address space: ``array[T, N]`` and ``array[T; N, N]``.

## Function type

- ``Fn[param, ...] @attrs -> ret`` A reference to a function that takes the given parameter types and returns ``ret``. The ``@arbitraryArgs`` attribute marks it variadic.