<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Compiler Directives

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``directive`` declaration applies a file-scoped compiler option from inside the source file. It is written at the top level and takes one null-terminated string literal with command-line spelling.

```thrust
directive "--disable-warnings=W0001";
directive "-opt=3";
```

The string must begin with ``-``. Flags that require a value accept either ``=`` or ``:`` as the separator.

```thrust
directive "-emit=llvm-ir";
directive "-print:tokens";
```

Directives only accept options that can be applied to one source file. Global-only compiler options are rejected.

Supported directive flags include:

- ``-opt``
- ``-reloc-model``
- ``-code-model``
- ``-dbg``
- ``-dbg-for-inlining``
- ``-dbg-for-profiling``
- ``-dbg-dwarf-version``
- ``-stop-at``
- ``-emit``
- ``-print``
- ``--stack-protector``
- ``--symbol-linkage-strategy``
- ``--denormal-floating-point-behavior``
- ``--denormal-floating-point-32-bits-behavior``
- ``--sanitizer``
- ``--no-sanitize``
- ``--disable-all-sanitizers``
- ``--disable-frame-pointer``
- ``--disable-uwtable``
- ``--disable-direct-access-external-data``
- ``--disable-rtlib-got``
- ``--disable-safe-trapping-math``
- ``--disable-safe-math``
- ``--disable-default-optimizations``
- ``--opt-passes``
- ``--modificator-opt-passes``
- ``--disable-warnings``
- ``--disable-all-warnings``
- ``--no-obfuscate-archive-names``
- ``--no-obfuscate-ir``

This syntax is **stable**.
