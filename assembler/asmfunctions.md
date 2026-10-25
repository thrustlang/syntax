<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Assembler Functions

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Assembler functions are functions written entirely in inline assembler. They support Intel and AT&T x86_64 assembler.

> [!WARNING]
> This syntax is **unstable**. It only works when the compiler runs in unstable mode, and it can change or disappear.

Assembler functions declare the parameter types inside parentheses and always declare a return type, including ``void``. The body is a raw ``#asm{...}`` block.

```thrust
asm fn add(s32, s32) s32 @public @asmSyntax("Intel") #asm{
    mov $0, $1,
    add $0, $2
}

fn main() s32 @public {
    return add(20, 22);
}
```

The raw block contains one assembler instruction per line. A trailing comma at the end of an instruction is removed by the lexer; commas between operands are preserved. The trailing comma on the last instruction is optional.

LLVM operand placeholders are numbered in constraint order:

- ``$0`` is the return value when the return type is not ``void``.
- The parameters start at ``$1`` when there is a return value.
- When the return type is ``void``, the parameters start at ``$0``.

The constraints are inferred from the signature. Non-void returns use ``=r`` (or ``=x`` for floating point), and parameters use ``r`` (or ``x`` for floating point). A trailing ``ret`` or ``retq`` instruction is ignored, because the compiler emits the function return after the inline assembler block.

Void assembler functions are allowed:

```thrust
asm fn touch() void @public #asm{
    nop
}
```

Global assembler also uses a raw block:

```thrust
global_asm #asm{
    .globl symbol,
    symbol:
}
```

## LLVM inline assembler

The syntax inside the assembler block follows the LLVM inline assembler format. For more information, see the LLVM language reference: <https://llvm.org/docs/LangRef.html>

<img src= "assets/LLVM-inline-assembler-ref.png" alt= "llvm-inline-assembler-ref" style= "width: 50%; height: 50%;"> </img>

Related unstable attributes: ``@asmSyntax("Intel" | "AT&T")``, ``@asmAlignStack``, ``@asmThrow``, ``@asmSideEffects``.
