<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Structures

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Structures behave like in C. They are traditional structures, a set of named fields with their own types.

## Memory information

- Allocation site: ``Stack or Heap``.
- Preferred allocation site: ``Stack``.

## Declaration

Fields are written as ``name: Type`` and separated by commas. A trailing comma is accepted.

```thrust
struct MyStruct @public {
    size: s64,
    length: s32,
    matter: bool
}
```

The ``@public`` attribute keeps the struct name in the output. The ``@packed`` attribute makes the compiler use a packed layout, without padding.

```thrust
struct PackedPoint @packed {
    x: u8,
    y: u32
}
```

Structs can be declared at the top level or inside a function body. They can also be generic.

```thrust
struct Wrapper[T] {
    value: T,
}
```

## Construction

A value is built with ``new``, giving each field by name.

```thrust
fn main() s32 @public {
    var some_struct: MyStruct = new MyStruct {
        matter: true,
        length: 12,
        size: 12312
    };

    return 0;
}
```

Fields are read and written with the dot operator.

```thrust
var some_size: s64 = some_struct.size;
some_struct.size = 2048;
```

## Property dereference

The arrow operator ``->`` reads or writes a field with an implicit dereference: ``v->a`` is sugar for ``deref v.a``. It works on struct values and on pointers to structs.

```thrust
fn main() s32 @public {
    var point: MyStruct = new MyStruct {
        matter: true,
        length: 12,
        size: 12312
    };

    var size: s64 = point->size;
    point->length = 13;

    return 0;
}
```

The arrow also composes with indexation. When a field is an array or a pointer, ``v->data->[2]`` reads the field and indexes it with an implicit dereference.

```thrust
struct Wrapper {
    data: ptr[array[s32; 4]],
}

fn main() s32 @public {
    var arr: array[s32; 4] = fixed[10, 20, 30, 40];
    var v := new Wrapper { data: ref arr };

    var element: s32 = v->data->[2];

    return 0;
}
```

This syntax is **stable**.
