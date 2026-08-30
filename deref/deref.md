<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# deref

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``deref`` expression loads a value from the memory a pointer points to. It unwraps one layer of pointer type, like ``*T`` in Rust.

It applies to:

- ``ptr[T]``
- ``ptr``

```thrust
fn main() s32 @public {
    var a: ptr[u32] = halloc(u32);

    var not_mutable_a: u32 = deref a;

    return 0;
}
```

The keyword can repeat to unwrap several layers: ``deref deref p``. It also accepts the same modificators as locals, such as ``volatile`` and the atomic ordering levels.

```thrust
var pointer: ptr[ptr[u32]] = halloc(ptr[u32]);
var value: u32 = deref deref pointer;
```

```thrust
var value: u32 = deref volatile pointer;
```

The opposite operation, taking the address of a value, is written with ``ref``.

```thrust
var pointer: ptr[u32] = ref a;
```

## load

The ``load`` expression loads the pointer value stored at the memory location of an operand. It always yields a pointer to the value, without dereferencing into it.

Like ``ref``, it keeps the type when it is already a pointer, and adds a pointer type when the operand is a value that lives in memory. It never unwraps a pointer layer.

```thrust
fn main() s32 @public {
    var a: s32 = 42;
    var p: ptr[s32] = ref a;

    var q: ptr[s32] = load p;

    return 0;
}
```

Here ``load p`` reads the ``ptr[s32]`` stored in the variable ``p``. This is different from ``deref p``, which would read the ``s32`` value that ``p`` points to.

It works on any operand that has a memory location: pointer variables, indexed array or pointer slots, and struct fields.

```thrust
fn main() s32 @public {
    var a: s32 = 10;
    var b: s32 = 20;

    var arr: array[ptr[s32]; 2] = fixed[ref a, ref b];

    var first: ptr[ptr[s32]] = load arr[0];

    return 0;
}
```

An operand that is a plain value without a memory address cannot be loaded; the compiler rejects it.

The keyword accepts the same modificators as ``deref`` and locals, such as ``volatile`` and the atomic ordering levels.

```thrust
var q: ptr[s32] = load volatile p;
```

This syntax is **stable**.