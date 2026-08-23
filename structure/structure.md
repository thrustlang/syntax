<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Structures

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Structures behave like in C. They are traditional structures, a set of named fields with their own types.

## Memory information

- Allocation site: ``Stack or Heap``.
- Preferred allocation site: ``Stack``.

## Declaration

Fields are written as ``name: Type`` and separated by commas.

```thrust
struct MyStruct @public {
    size: s64,
    length: s32,
    matter: bool
}
```

The ``@public`` attribute keeps the struct name in the output. The ``@packed`` attribute makes the compiler use a packed layout, without padding.

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

Fields are read with the dot operator: ``some_struct.size``.

This syntax is **stable**.