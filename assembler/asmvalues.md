<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Assembler Values

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Assembler values are blocks of code written entirely in assembler that can be used as normal values in the language. They carry a type, optional arguments, and two blocks for the assembler lines and the constraints.

> [!WARNING]
> This syntax is **unstable**. It only works when the compiler runs in unstable mode, and it can change or disappear.

```thrust
fn main() s32 @public {
    var whatever: u32 = asm u32 {
        "mov $$42, %eax"
    } {
        ""
    } + 20;

    return 0;
}
```

Assembler values can take attributes after the type and before the argument list or assembler block. They can also take arguments inside parentheses after the type, separated by ``:``.

```thrust
fn main() s32 @public {
    var a: u32 = 2;
    var b: u32 = 3;

    var result: u32 = asm u32 @asmSyntax("Intel") (a : b) {
        "mov $1, %eax",
        "add $2, %eax"
    } {
        "=r",
        "r",
        "r"
    };

    return 0;
}
```

> [!NOTE]
> The current parser has an implementation discrepancy around null-terminated and non-null-terminated string tokens in assembler constraints. Treat this syntax as unstable and prefer normal string literals until the parser behavior is finalized.

## LLVM inline assembler

The syntax inside the assembler strings follows the LLVM inline assembler format. For more information, see the LLVM language reference: <https://llvm.org/docs/LangRef.html>

<img src= "assets/LLVM-inline-assembler-ref.png" alt= "llvm-inline-assembler-ref" style= "width: 50%; height: 50%;"> </img>
