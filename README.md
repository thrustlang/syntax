<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Thrust Programming Language - Syntax

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

This repository holds detailed and general information about the syntax of the **Thrust** programming language. It is not user documentation as such; it is a guide for developing the compiler and the language. The authoritative implementation is the [Thrust Compiler](https://github.com/thrustlang/thrustc).

> [!IMPORTANT]
> The compiler is in deep, constant development. A syntax marked as **stable** is considered final and only receives bug fixes. That does not mean it is free of issues in edge cases. A syntax marked as **unstable** can change or disappear without notice.

## Stable and unstable syntax

The compiler has two feature modes:

- **Stable.** The syntax is recognized in the default mode. It is considered final, subject only to bug fixes. Keep in mind that the compiler is still maturing, so even stable syntax can hit issues in edge cases.
- **Unstable.** The syntax is only recognized when the compiler runs in unstable mode. It is experimental, can change, and can be removed at any time. Assembler constructs (``asmfn``, ``asm``, ``global_asm``), ``embedded``, ``importC``, and the ``@asm*`` and ``@promote`` attributes are unstable. ``importC`` is still in development.

Each page in this repository marks what it documents as stable or unstable.

## Current language surface

The compiler recognizes these stable top-level declarations:

- ``type`` Type aliases.
- ``struct`` Structures.
- ``const`` Compile-time constants.
- ``static`` Static storage.
- ``enum`` Enumerations.
- ``fn`` Functions and prototypes.
- ``intrinsic`` Compiler intrinsic declarations.
- ``import`` Module imports.
- ``directive`` Compiler directives.
- ``@if`` / ``@elif`` / ``@else`` Compile-time conditional declarations.

The unstable top-level declarations are ``asmfn``, ``global_asm``, ``embedded``, and ``importC``. The ``asm`` expression is also unstable.

Stable statement forms include blocks, ``return``, local ``static``, local ``const``, local ``struct``, local ``type``, local ``enum``, ``var``, ``if`` / ``elif`` / ``else``, ``@if`` / ``@elif`` / ``@else``, ``for``, ``while``, ``loop``, ``continue``, ``continueall``, ``break``, ``breakall``, ``defer``, and expression statements.

The lexer reserves these stable keywords and literals: ``var``, ``fn``, ``if``, ``elif``, ``else``, ``for``, ``while``, ``loop``, ``true``, ``false``, ``or``, ``and``, ``const``, ``struct``, ``return``, ``break``, ``continue``, ``breakall``, ``continueall``, ``defer``, ``pass``, ``nullptr``, ``as``, ``deref``, ``type``, ``enum``, ``alloc``, ``address``, ``addr``, ``load``, ``write``, ``fixed``, ``ref``, ``mut``, ``static``, ``unreachable``, ``intrinsic``, ``new``, ``import``, ``only``, and ``directive``.

The lexer reserves these unstable keywords when unstable mode is enabled: ``asmfn``, ``asm``, ``global_asm``, ``embedded``, and ``importC``.

> [!NOTE]
> ``alloc``, ``address``, ``addr``, and ``write`` are reserved by the lexer, but their user-facing syntax is not fully specified yet.

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
- ``modules/`` Importing code between files and modules, and file-scoped compiler directives.
- ``statements/`` Conditional statements, compile-time conditionals, and deferred execution.
- ``structure/`` Traditional structures.
- ``generics/`` Generics types.
- ``types/`` Native and primitive types of the language, and type aliases.
- ``variables/`` Types of variables, their mutation, and statics.
