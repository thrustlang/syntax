<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Attributes

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Attributes are compile-time code generation modifiers. They change how the compiler builds the code, how the code runs, its visibility, and its calling convention.

This page separates the attributes into **stable** and **unstable**. The unstable attributes only work when the compiler runs in unstable mode.

## Stable attributes

### Visibility

- ``@public`` Keeps the plain name of a function, intrinsic, static, constant, struct, enum, or type alias in the output. Without it, exported symbols can get an obfuscated name.
- ``@entrypoint`` Marks an entry-point candidate. It is recognized by the lexer and attribute parser, but its final semantics are still implementation-defined.

```thrust
fn main() s32 @public {
    return 0;
}
```

### Memory and layout

- ``@heap`` Allocates the value on the heap.
- ``@dealloc`` On a local variable, schedules automatic deallocation at scope exit. On a function, use ``@deallocator`` instead.
- ``@dealloc(function)`` or ``@dealloc(module::function)`` On a local variable, schedules a specific cleanup function at scope exit.
- ``@deallocator`` Marks a function as the deallocator for the type of its single pointer parameter.
- ``@align(N)`` Sets the alignment of the value to ``N``. The compiler expects a literal unsigned integer. The semantic checker accepts power-of-two alignments up to ``128``.
- ``@packed`` Uses a packed layout for a struct, without padding.

```thrust
fn dropBuffer(buffer: ptr[Buffer]) void @public @deallocator {
    mem::freeMemory(buffer->data);
}

fn main() s32 @public {
    var buffer @dealloc := newBuffer();
    var raw @dealloc(mem::freeMemory): ptr = mem::allocateMemory(64);

    return 0;
}
```

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

- ``@extern("name")`` Binds a function, static, or constant to the external symbol ``name``. External symbols must also be public. See ``function/ffi.md``.
- ``@linkage("kind")`` Sets the linkage kind. Accepted names are ``"standard"``, ``"common"``, ``"dllimport"``, ``"dllexport"``, ``"externweak"``, ``"weak"``, ``"internal"``, ``"linkerprivate"``, and ``"linkerprivateweak"``.
- ``@convention("name")`` Sets the calling convention. See the list below.
- ``@arbitraryArgs`` Marks a function as variadic. See ``function/function.md``.

Variadic prototypes without a body normally represent external functions and therefore use ``@extern``. Named arguments are not supported on calls to variadic functions.

### Compile-time conditionals

- ``@if``, ``@elif``, ``@else`` Select code at compile time. See ``statements/compiletime.md``.

## Unstable attributes

- ``@promote(T -> U, ...)`` Promotes variadic argument types before a call is lowered.
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

The full accepted list also includes ``GraalVM``, ``X86StdCall``, ``X86FastCall``, ``X86ThisCall``, ``X86VectorCall``, ``X86RegCall``, ``X86_64_SysV``, ``ARMAPCS``, ``ARMAAPCS``, ``ARM_AAPCS_VFP``, ``AArch64VectorCall``, ``AArch64SVEVectorCall``, ``SwiftTail``, ``PreserveNone``, ``AnyReg``, ``PTXKernel``, ``PTXDevice``, ``AMDGPUKernel``, ``AMDGPUGfx``, ``RISCVVectorCall``, ``CPPFastTLS``, ``CFGuardCheck``, ``MSP430_INTR``, ``SPIRFunc``, ``SPIRKernel``, ``Intel_OCL_BI``, ``X86_INTR``, ``AVR_INTR``, ``AVR_SIGNAL``, ``AVR_BUILTIN``, ``AMDGPU_VS``, ``AMDGPU_GS``, ``AMDGPU_PS``, ``AMDGPU_CS``, ``AMDGPU_HS``, ``MSP430_BUILTIN``, ``AMDGPU_LS``, ``AMDGPU_ES``, ``WebAssembly``, ``M68k_INTR``, ``M68k_RTD``, ``ARM64ECThunkX64``, ``ARM64ECThunkNative``, ``AMDGPUCSChain``, ``AMDGPUCSChainPreserve``, ``AMDGPU_Gfx_WholeWave``, ``CHERIoT_CompartmentCall``, ``CHERIoTCompartmentCallee``, ``CHERIoTLibraryCall``, and the ``RISCV_VLSCall_*`` and ``AArch64SMEABISupportRoutines*`` target-specific names.

## Attribute parsing notes

Attributes are parsed in declaration-specific positions. Repeating the same semantic attribute on one item is rejected by the attribute checker.

```thrust
fn f(a: u32, b: u32) u32 @convention("C") @public {
    return a + b;
}
```
