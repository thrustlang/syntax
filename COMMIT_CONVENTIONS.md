<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Thrust Programming Language - Syntax

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

A simple guide of standard conventions to follow in order to deliver a good Github commit for the Thrust Syntax repository.

### Title

It needs to be detailed. It can include a lot of technical slang. A well designed Github commit title always needs a specific syntax:

#### Title - features

Following the syntax:

`feat(...)`

Valid locations:

- `assembler` Any location that usually involves pure assembler-type functions and assembler values treated as conventional expressions.
- `attributes` Any location that usually involves the compile-time code generation modifiers.
- `builtins` Any location that usually involves built-in functions.
- `types` Any location that usually involves native and primitive types, casts, type aliases, and constants.
- `variables` Any location that usually involves types of variables, their mutation, and statics.
- `functions` Any location that usually involves functions, the foreign function interface (FFI), and compiler intrinsics.
- `modules` Any location that usually involves importing code between files and modules.
- `memory` Any location that usually involves high-level pointer dereferencing.
- `control_flow` Any location that usually involves conditionals, deferred execution, and traditional loops such as `for`, `while`, and `loop`.
- `structure` Any location that usually involves structures and enums.
- `project` Any location that usually involves the repository itself: `README.md`, `LICENSE.txt`, `assets/`, or the conception of a new part of the syntax repository.

Example:

`feat(modules)` Adding the documentation of the import statement and module system.

#### Title - fixes

Following the syntax:

`fix(...)`

Valid locations:

- `assembler` Any location that usually involves pure assembler-type functions and assembler values treated as conventional expressions.
- `attributes` Any location that usually involves the compile-time code generation modifiers.
- `builtins` Any location that usually involves built-in functions.
- `types` Any location that usually involves native and primitive types, casts, type aliases, and constants.
- `variables` Any location that usually involves types of variables, their mutation, and statics.
- `functions` Any location that usually involves functions, the foreign function interface (FFI), and compiler intrinsics.
- `modules` Any location that usually involves importing code between files and modules.
- `memory` Any location that usually involves high-level pointer dereferencing.
- `control_flow` Any location that usually involves conditionals, deferred execution, and traditional loops such as `for`, `while`, and `loop`.
- `structure` Any location that usually involves structures and enums.
- `project` Any location that usually involves the repository itself: `README.md`, `LICENSE.txt`, `assets/`, or the conception of a new part of the syntax repository.

Any consecutive location written next to another needs to be followed by a COMMA character `,`.

Example:

`fix(types)` Fixing the return type of `sizeOf(T)`.

#### Title - Combinatory

In order to create a well designed combinatory title, you need to use the following syntax:

`(feat(...), fix(...))`

- It needs to be encapsulated by a pair of PAREN characters `()`.
- Each next feature or fix needs to be followed by a COMMA character `,`.

### Description

It needs to be concise and short, but detailed at the same time. It can include a lot of technical slang.