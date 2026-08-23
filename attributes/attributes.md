<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Attributes

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Attributes are compile-time code generation modifiers. They change how the compiler builds the code, how the code runs, its visibility, and its calling convention.

This page separates the attributes into **stable** and **unstable**. The unstable attributes only work when the compiler runs in unstable mode.

## Stable attributes

### Visibility

- ``@public`` Keeps the plain name of the structure in the output. Without it, functions and constants get an obfuscated name.

```thrust
fn main() s32 @public {
    return 0;
}
```

### Memory and layout

- ``@heap`` Allocates the value on the heap.
- ``@align(N)`` Sets the alignment of the value to ``N``.
- ``@packed`` Uses a packed layout for a struct, without padding.

### Code generation

- ``@hot`` Marks a function as frequently executed, favoring performance.
- ``@minSize`` Optimizes the function for the smallest code size.
- ``@noInline`` Prevents the function from being inlined.
- ``@inline`` Suggests inlining.
- ``@alwaysInline`` Forces inlining at every call site.
- ``@safeStack`` Uses a separate stack for sensitive data.
- ``@weakStack`` Applies light stack protection.
- ``@strongStack`` Applies strong stack protection.
- ``@preciseFloatingPoint`` Keeps floating-point operations precise.
- ``@noUnwind`` States the function does not unwind the stack.
- ``@noReturn`` States the function does not return.
- ``@optFuzzing`` Marks the function for fuzzing-related optimization.
- ``@pure`` Marks the function as pure.
- ``@thunk`` Marks the function as a thunk.
- ``@cuda`` Marks the function as a CUDA kernel.
- ``@constructor`` Runs the function at load time.
- ``@destructor`` Runs the function at unload time.

### Symbols and calling

- ``@extern("name")`` Binds the function to the external symbol ``name``. See ``function/ffi.md``.
- ``@linkage("kind")`` Sets the linkage kind, for example ``"internal"``, ``"weak"``, or ``"common"``.
- ``@convention("name")`` Sets the calling convention. See the list below.
- ``@arbitraryArgs`` Marks a function as variadic. See ``function/function.md``.

### Compile-time conditionals

- ``@if``, ``@elif``, ``@else`` Select code at compile time. See ``statements/compiletime.md``.

## Unstable attributes

- ``@promote`` Promotes a value between two types.
- ``@asmAlignStack`` Aligns the stack for an assembler block.
- ``@asmSyntax("Intel" | "AT&T")`` Chooses the inline assembler syntax.
- ``@asmThrowErrors`` Lets assembler errors propagate.
- ``@asmSideEffects`` Tells the backend the assembler block has side effects.

These apply to the assembler constructs in ``assembler/``, which are also unstable.

## Calling conventions

The ``@convention`` attribute accepts a wide set of names. The common ones:

- ``"C"`` The C calling convention.
- ``"fast"`` Fast calling, favors registers.
- ``"tail"`` Enables tail call optimization.
- ``"cold"`` For rarely called functions.
- ``"weakReg"`` Preserves most caller-saved registers.
- ``"strongReg"`` Preserves all caller-saved registers.
- ``"Swift"`` The Swift convention.
- ``"Haskell"`` The Glasgow Haskell Compiler convention.
- ``"Erlang"`` The High-Performance Erlang Compiler convention.
- ``"Win64"`` The Windows x64 convention.

The full accepted list also includes ``X86StdCall``, ``X86FastCall``, ``X86ThisCall``, ``X86VectorCall``, ``X86RegCall``, ``X86_64_SysV``, ``ARMAPCS``, ``ARMAAPCS``, ``AArch64VectorCall``, ``AArch64SVEVectorCall``, ``SwiftTail``, ``PreserveNone``, ``AnyReg``, ``PTXKernel``, ``PTXDevice``, ``AMDGPUKernel``, ``AMDGPUGfx``, ``RISCVVectorCall``, ``WebAssembly``, and many target-specific names.

```thrust
fn f(a: u32, b: u32) u32 @convention("C") @public {
    return a + b;
}
```