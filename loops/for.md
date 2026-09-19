<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# For Loop

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``for`` loop is very close to the C loop, with a slightly altered syntax. It declares a local, a condition, and an action, each separated by ``;``.

```thrust
for var i: u32 = 0; i < 1000; i++; {
    // loop body
}
```

Notice the action ends with ``;`` before the block opens. Without the declaration part, ``for`` also works as an infinite loop, like ``loop``.

The action accepts expressions and statements. Simple statements keep their trailing ``;``. Compound statements, such as blocks and conditionals, are followed directly by the loop body.

```thrust
for var i: u32 = 0; i < 10; {
    i += 1;
} {
    // loop body
}

for var i: u32 = 0; i < 10; if i == 5 {
    i += 2;
} else {
    i += 1;
} {
    // loop body
}
```

```thrust
for {
    // infinite loop
}
```

The semicolon-only form also creates an infinite loop and accepts a block or a single statement body.

```thrust
for ;;; {
    // infinite loop
}

for ;;; break;
```

A full ``for`` can also use a single statement body.

```thrust
for var i: u32 = 0; i < 10; i++; total += i;
```

This syntax is **stable**.
