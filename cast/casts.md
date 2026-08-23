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

This syntax is **stable**.