<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Casts

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Casting transforms a value from one type to another. The compiler checks at compile time whether the conversion is possible. It is equivalent to the ``as`` keyword in Rust.

```thrust
fn main() s32 @public {
    var a: u32 = 100;

    var b: ptr[u32] = a as ptr[u32];

    return 0;
}
```

Casting is also useful to move between pointer types, for example when a function asks for a plain ``ptr``.

```thrust
fn main() s32 @public {
    var a: ptr[u32] = halloc(u32);
    memset(a as ptr, 0, sizeOf(u32));
    return 0;
}
```

## Pointers and stored values

A cast reads a value. It does not implicitly load a pointer stored inside another value.

``ptr``, ``ptr[T]``, and ``Fn[...]`` are pointer values. Casting one of them to another pointer type, to an integer, or to an array type uses the pointer value itself.

```thrust
fn main() s32 @public {
    var value: s32 = 42;
    var p: ptr[s32] = ref value;
    var raw: ptr = p as ptr;
    var rawAddress: usize = p as usize;

    return 0;
}
```

``raw`` has the same address as ``p``. ``rawAddress`` is that address as an integer.

Array values (``array[T]``, ``array[T; N]``, and ``CString``) are stored objects, not pointer values. Casting one of them to a pointer uses the address of the array object in the current storage. It does not follow a pointer stored inside the object.

```thrust
fn main() s32 @public {
    var text: CString = "hello";
    var raw: ptr[char] = text as ptr[char];

    return 0;
}
```

Here ``raw`` refers to the storage of the ``text`` object. It is not necessarily the address of the characters in ``"hello"``. The storage is the local slot, a parameter, a static, or a literal, depending on where the array value lives.

If a function returns a pointer and you need an array view, cast the pointer value to the array type.

```thrust
fn asText(value: ptr[char]) CString {
    return value as CString;
}
```

Use ``ref``, ``load``, and ``deref`` when you need to choose explicitly between an object's address and the value stored in it. See ``spec/deref/deref.md``.

## Comparisons after a cast

The comparison operators see the value a cast produces. Pointer equality compares pointer values.

```thrust
fn main() s32 @public {
    var value: s32 = 42;
    var p: ptr[s32] = ref value;
    var raw: ptr = p as ptr;

    if raw == nullptr { return 1; }
    if raw != p { return 2; }

    return 0;
}
```

``ptr`` and ``ptr[T]`` support ``==`` and ``!=``. Ordering comparisons such as ``<`` and ``>`` are not defined for pointers.

Arrays and ``CString`` values are not pointer values for comparison. Cast one to a pointer first, or compare the contents with the library function for that array type. Casting a local ``CString`` to a pointer and comparing the result with ``nullptr`` checks the address of the array storage, not the pointer stored inside it.

```thrust
fn main() s32 @public {
    var text: CString = "hello";

    if (text as ptr[char]) == nullptr {
        return 1;
    }

    return 0;
}
```

The condition above checks the address of ``text``. For a null check, compare a pointer value rather than an array cast.

```thrust
fn main() s32 @public {
    var value: ptr[char] = nullptr;

    if value == nullptr {
        return 1;
    }

    return 0;
}
```

This syntax is **stable**.
