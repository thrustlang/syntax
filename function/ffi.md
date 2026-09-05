<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Foreign Function Interface (FFI)

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The foreign function interface lets Thrust call code written in another language, usually C. It works by declaring a function prototype and telling the compiler which external symbol to use.

## The ``@extern`` attribute

``@extern("name")`` names the external symbol that the compiler looks for at call time. It only applies to functions. A function without ``@public`` or ``@extern`` gets an obfuscated name in the output, so it is not meant to be seen from outside.

```thrust
fn sum(a: u64, b: u64) u64 @public @extern("sum_c");
```

## Calling conventions

The ``@convention("name")`` attribute sets how arguments and return values pass between caller and callee. The most common is the C convention.

```thrust
fn printf(fmt: const array[char]) s32 @public @arbitraryArgs @extern("printf") @convention("C");
```

## Other attributes

- ``@public`` keeps the plain function name in the output.
- ``@linkage("kind")`` sets the linkage, for example ``"internal"`` or ``"weak"``.
- ``@arbitraryArgs`` marks the function as variadic, as in ``printf``.

```thrust
fn hidden_sum(a: u64, b: u64) u64 @public @extern("hidden_sum") @linkage("internal");
```

This syntax is **stable**. For importing whole C libraries at once, see ``importC`` in ``modules/import.md``, which is **in development**.