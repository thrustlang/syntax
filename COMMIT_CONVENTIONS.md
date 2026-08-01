<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/thrustlang-logo-name.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# The Thrust Syntax

<img src="https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt="standard-separator" style="width: 1hv;">

There is a simple guide of standard conventions to follow in order to delivery a good Github commit for the Thrust Syntax repository.

### Title

It needs to be detailed. It can be include a lot of technical slang. The base of a well designed Github commit title always will be and needs a specific syntax as:

#### Title - features

Following the syntax:

`feat(...)`

Valid locations:

- `assembler` Any location that usually involucrates pure assembler-type functions and assembler values treated as conventional expressions.
- `attributes` Any location that usually involucrates the compile-time code generation modifiers.
- `builtins` Any location that usually involucrates built-in functions such as `sizeof`, `alignof`, `memcpy`, `memmove` and `memset`.
- `types` Any location that usually involucrates native and primitive types, casts and constants.
- `variables` Any location that usually involucrates types of variables and their mutation.
- `functions` Any location that usually involucrates functions and the Foreign Function Interface (FFI).
- `memory` Any location that usually involucrates high-level pointer dereferencing and low-level instructions (LLI).
- `control_flow` Any location that usually involucrates traditional loops such as `for`, `while` and `loop {}`.
- `structure` Any location that usually involucrates structures and enums.
- `project` Any location that usually involucrates the repository itself: `README.md`, `LICENSE.txt`, `assets/`, or the conception of a new part of the syntax repository.

Example:

`feat(memory)` Adding the explicit memory overwriting instructions to the LLI documentation.

#### Title - fixes

Following the syntax:

`fix(...)`

Valid locations:

- `assembler` Any location that usually involucrates pure assembler-type functions and assembler values treated as conventional expressions.
- `attributes` Any location that usually involucrates the compile-time code generation modifiers.
- `builtins` Any location that usually involucrates built-in functions such as `sizeof`, `alignof`, `memcpy`, `memmove` and `memset`.
- `types` Any location that usually involucrates native and primitive types, casts and constants.
- `variables` Any location that usually involucrates types of variables and their mutation.
- `functions` Any location that usually involucrates functions and the Foreign Function Interface (FFI).
- `memory` Any location that usually involucrates high-level pointer dereferencing and low-level instructions (LLI).
- `control_flow` Any location that usually involucrates traditional loops such as `for`, `while` and `loop {}`.
- `structure` Any location that usually involucrates structures and enums.
- `project` Any location that usually involucrates the repository itself: `README.md`, `LICENSE.txt`, `assets/`, or the conception of a new part of the syntax repository.

Any consecutive location written to the next one needs to be follow for a COMMA character `,`.

Example:

`fix(builtins)` Fixing the return type of `sizeof(T) u32`.

#### Title - Combinatory

In order to create a well disigned combinatory title, you need to use the following syntax:

`(feat(...), fix(...))`

- It needs to be encapsulated for a pair characters PAREN `()`.
- Each next feature or fix needs to be followed for a COMMA character `,`.

### Description

It needs to be concise, short, but detailed in the same time. It can be include a lot of technical slang.
