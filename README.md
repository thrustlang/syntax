<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Thrust Programming Language - Syntax

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

This repository holds detailed and general information about the syntax of the **Thrust** programming language. It is not user documentation as such; it is a guide for developing the compiler and the language. The authoritative implementation is the [Thrust Compiler](https://github.com/thrustlang/thrustc).

> [!IMPORTANT]
> The compiler is in deep, constant development. A syntax marked as **stable** is considered final and only receives bug fixes. That does not mean it is free of issues in edge cases. A syntax marked as **unstable** can change or disappear without notice.

## Stable and unstable syntax

The compiler has two feature modes:

- **Stable.** The syntax is recognized in the default mode. It is considered final, subject only to bug fixes. Keep in mind that the compiler is still maturing, so even stable syntax can hit issues in edge cases.
- **Unstable.** The syntax is only recognized when the compiler runs in unstable mode. It is experimental, can change, and can be removed at any time. Assembler constructs (`asmfn`, `asm`, `global_asm`), `embedded`, `importC`, and the `@asm*` and `@promote` attributes are unstable.

Each page in this repository marks what it documents as stable or unstable.

## Content

- ``assembler/`` Information about pure assembler-type functions and assembler values treated as conventional expressions. Unstable.
- ``attributes/`` Attributes are compile-time code generation modifiers that can change the behavior of code.
- ``builtins/`` Built-in functions that are part of the compiler and the language.
- ``cast/`` Compile-time type transformation.
- ``constants/`` Traditional constants.
- ``deref/`` High-level pointer dereferencing with ``deref``, ``ref`` and ``load``.
- ``enum/`` Traditional enum.
- ``function/`` Functions, the foreign function interface (FFI), and compiler intrinsics.
- ``loops/`` Traditional loops such as `for`, `while`, and `loop`, with their control flow.
- ``modules/`` Importing code between files and modules.
- ``statements/`` Conditional statements, compile-time conditionals, and deferred execution.
- ``structure/`` Traditional structures.
- ``types/`` Native and primitive types of the language, and type aliases.
- ``variables/`` Types of variables, their mutation, and statics.