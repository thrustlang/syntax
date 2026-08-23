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
var value: u32 = deref volatile pointer;
```

The opposite operation, taking the address of a value, is written with ``ref``.

```thrust
var pointer: ptr[u32] = ref a;
```

This syntax is **stable**.