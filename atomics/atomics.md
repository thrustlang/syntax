<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Atomic Operations

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The atomic builtins perform read-modify-write and compare-and-swap operations on a memory location. They map to the LLVM ``atomicrmw`` and ``cmpxchg`` instructions.

## Declaring an atomic destination

The destination of an atomic operation must be a variable declared with an atomic ordering modificator:

```thrust
var atomicRelax counter: u32 = 0;
static mut atomicSync shared: u64 = 0;
```

The operation inherits the ordering from the destination declaration. ``atomicNone`` and ``atomicFree`` do not describe an atomic memory operation and are rejected on atomic builtins.

## Read-modify-write builtins

Each read-modify-write builtin writes a value into the destination atomically and returns the previous value:

| Builtin | LLVM | Meaning |
|---|---|---|
| ``atomicStore(counter, value)`` | xchg | Store a new value, returns the previous one |
| ``atomicAdd(counter, value)`` | add | Addition |
| ``atomicSubtract(counter, value)`` | sub | Subtraction |
| ``atomicAnd(counter, value)`` | and | Bitwise and |
| ``atomicNand(counter, value)`` | nand | Bitwise nand |
| ``atomicOr(counter, value)`` | or | Bitwise or |
| ``atomicXor(counter, value)`` | xor | Bitwise xor |
| ``atomicSignedMaximum(counter, value)`` | max | Signed maximum |
| ``atomicSignedMinimum(counter, value)`` | min | Signed minimum |
| ``atomicUnsignedMaximum(counter, value)`` | umax | Unsigned maximum |
| ``atomicUnsignedMinimum(counter, value)`` | umin | Unsigned minimum |

The destination and the value must be integers.

```thrust
fn main() s32 @public {
    var atomicRelax counter: u32 = 10;

    var old: u32 = atomicAdd(counter, 5);   // old == 10
    if counter != 15 { return 1; }

    var previous: u32 = atomicStore(counter, 50);   // previous == 15
    if counter != 50 { return 2; }

    return 0;
}
```

## Compare-and-swap

``atomicCompareAndSwap`` compares the destination against an expected value, and swaps in a new value when they match. It follows the C11 model: ``expected`` is passed by address and is updated with the current value when the comparison fails. The builtin returns a boolean that is ``true`` when the swap happened.

```thrust
atomicCompareAndSwap(counter, expected, new, success, failure)
```

- ``counter`` The destination memory location.
- ``expected`` An lvalue holding the expected value; updated on failure.
- ``new`` The value stored on success.
- ``success`` and ``failure`` Atomic ordering arguments, using the atomic keyword literals.

```thrust
fn main() s32 @public {
    var atomicRelax counter: u32 = 20;

    var expected: u32 = 20;
    var swapped: bool = atomicCompareAndSwap(counter, expected, 30, atomicSync, atomicRelax);

    if !swapped { return 1; }        // matched, counter is now 30
    if counter != 30 { return 2; }

    expected = 99;
    swapped = atomicCompareAndSwap(counter, expected, 40, atomicSync, atomicRelax);

    if swapped { return 3; }         // did not match, counter stays 30
    if expected != 30 { return 4; }  // expected received the current value
    if counter != 30 { return 5; }

    return 0;
}
```

## Ordering rules

The compiler rejects, with ``E0056``, orderings that LLVM cannot lower:

- The success and failure orderings must be at least ``atomicRelax``.
- The failure ordering cannot be ``atomicDrop`` (release) or ``atomicSync`` (acquire-release).
- The failure ordering cannot be stronger than the success ordering.

This syntax is **unstable**.