<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Compile-time Conditionals

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``@if``, ``@elif``, and ``@else`` attributes pick code at compile time. The condition must fold to a constant boolean, and the branch that is not taken is dropped before code generation. This is how the same source can adapt to the target platform.

The condition can use the target builtins from ``builtins/README.md``, such as ``isLinux()`` or ``is64Bit()``.

## Inside a function

```thrust
fn main() s32 @public {
    var count: s32 = 0;

    @if(false) {
        count += 1;
    } @elif(true) {
        count += 2;
    } @else {
        count += 100;
    }

    return 0;
}
```

The branches can also hold a single statement without braces.

```thrust
@if(true) var a: s32 = 5; @else var a: s32 = 9999;
```

## At the top level

Compile-time conditionals also work at the top level, selecting between functions, constants, statics, and imports.

```thrust
@if(isWindows()) import "win.thrust" only { platform };
@elif(isLinux()) import "linux.thrust" only { platform };
@else import "other.thrust" only { platform };
```

```thrust
@if(true) fn active_fn() s32 { return 100; }
@else fn inactive_fn() s32 { return 9999; }
```

```thrust
@if(isLinux()) const PLATFORM: u32 = 2;
@elif(isWindows()) const PLATFORM: u32 = 1;
@else const PLATFORM: u32 = 3;
```

The compiler only type-checks the branch that stays. A branch that will be dropped can contain code that would not compile on its own.

```thrust
@if(false) {
    var only_on_false: s32 = not_a_real_function();
}
```

This syntax is **stable**.