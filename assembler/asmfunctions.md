<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Assembler Functions

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Assembler functions are functions written entirely in inline assembler. They support Intel and AT&T x86_64 assembler.

> [!WARNING]
> This syntax is **unstable**. It only works when the compiler runs in unstable mode, and it can change or disappear.

The body has two blocks. The first block holds the assembler lines, each as a null-terminated string. The second block holds the constraints.

```thrust
asmfn invoke_exit_syscall() void {
    "mov $$60, %rax",
    "mov $$1, %rdi",
    "syscall"
} {
    "~{rax}~{rdi}"
}

fn main() s32 @public {
    invoke_exit_syscall();
    return 0;
}
```

Assembler functions accept parameters, a return type, and attributes, like normal functions.

```thrust
asmfn add(a u32, b u32) u32 @public @asmSyntax("Intel") {
    "mov %eax, $0"
} {
    "=r"
}
```

Unlike normal ``fn`` declarations, the current ``asmfn`` parser expects assembler parameters as ``name Type`` without a colon. This is unstable and may change.

Global assembler is written at the top level with ``global_asm``.

```thrust
global_asm(".globl symbol");
```

## LLVM inline assembler

The syntax inside the assembler strings follows the LLVM inline assembler format. For more information, see the LLVM language reference: <https://llvm.org/docs/LangRef.html>

<img src= "assets/LLVM-inline-assembler-ref.png" alt= "llvm-inline-assembler-ref" style= "width: 50%; height: 50%;"> </img>

Related unstable attributes: ``@asmSyntax("Intel" | "AT&T")``, ``@asmAlignStack``, ``@asmThrow``, ``@asmEffects``.
