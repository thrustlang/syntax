<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Compiler Intrinsics

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``intrinsic`` declaration binds a function to a compiler intrinsic, giving it an internal LLVM name while exposing a Thrust name. It is declared like a function prototype.

```thrust
intrinsic("llvm.assume") assume(condition: bool) void @public;
intrinsic("llvm.sqrt.f32") sqrt(value: f32) f32 @public;
```

The first string is the LLVM intrinsic name, the identifier after it is the name used in Thrust code, and the rest is the parameter list, return type, attributes, and final semicolon. The return type is always explicit, including ``void``.

Intrinsics should be public and do not support named arguments at call sites.

```thrust
fn main() s32 @public {
    var x: f32 = sqrt(16.0);
    return 0;
}
```

This syntax is **stable**. The list of valid LLVM intrinsic names lives in the LLVM language reference: <https://llvm.org/docs/LangRef.html>.
