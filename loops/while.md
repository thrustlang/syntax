<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# While Loop

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``while`` loop runs its block as long as the condition is true.

```thrust
var c: u32 = 1231;

while c != 100_000 {
    c++;
}
```

A ``while`` can also carry a local declaration, written before the condition. The local lives only inside the loop.

```thrust
while var i: u32 = 0; i < 100; {
    // loop body
    i++;
}
```

A normal ``while`` requires a block body. The ``while var`` form can use either a block or a single statement after the condition.

This syntax is **stable**.
