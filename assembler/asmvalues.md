<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Assembler Values

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Assembler values are blocks of inline assembler that can be used as normal expressions. They declare the parameter types, a return type, and the arguments passed to the block.

> [!WARNING]
> This syntax is **unstable**. It only works when the compiler runs in unstable mode, and it can change or disappear.

The return type is always required, including ``void``. Arguments are written after the raw ``#asm{...}`` block.

```thrust
fn main() s32 @public {
    var left: s32 = 20;
    var right: s32 = 22;

    var result: s32 = asm (s32, s32) s32 #asm{
        mov $0, $1,
        add $0, $2
    } (left, right);

    return result;
}
```

An assembler value can also return ``void`` and be used as a statement:

```thrust
fn main() s32 @public {
    asm () void #asm{
        nop
    } ();

    return 0;
}
```

The raw block contains one assembler instruction per line. A trailing comma at the end of an instruction is removed by the lexer; commas between operands are preserved. The trailing comma on the last instruction is optional.

LLVM operand placeholders are numbered in constraint order:

- ``$0`` is the return value when the return type is not ``void``.
- The arguments start at ``$1`` when there is a return value.
- When the return type is ``void``, the arguments start at ``$0``.

The constraints are inferred from the signature. Non-void returns use ``=r`` (or ``=x`` for floating point), and parameters use ``r`` (or ``x`` for floating point). Attributes may be placed after the return type and before the raw block.

A trailing ``ret`` or ``retq`` instruction is ignored, because the assembler value continues the surrounding function after the block.

## LLVM inline assembler

The syntax inside the assembler block follows the LLVM inline assembler format. For more information, see the LLVM language reference: <https://llvm.org/docs/LangRef.html>

<img src= "assets/LLVM-inline-assembler-ref.png" alt= "llvm-inline-assembler-ref" style= "width: 50%; height: 50%;"> </img>
