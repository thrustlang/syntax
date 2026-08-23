<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Enums

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Enums hold named variants. Each variant has a type and a value, written as ``Name: Type = value;`` and separated by semicolons.

```thrust
enum Colors @public {
    Red: u32 = 0;
    Yellow: u32 = 1;
    Blue: u32 = 2;
}
```

A variant value is read with the arrow operator: ``Colors->Yellow``. It behaves like a constant, so it can be used in expressions.

```thrust
fn main() s32 @public {
    var yellow_plus_red: u32 = Colors->Yellow + Colors->Red;
    return 0;
}
```

This syntax is **stable**.