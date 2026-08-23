<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Continue | Loop Control Flow

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

``continue`` jumps to the next iteration of the loop, skipping the rest of the block. It behaves the same as in C.

```thrust
for var i: u32 = 0; i < 1000; i++; {
    if i >= 666 {
        continue;
    }
}
```

``continueall`` skips to the next iteration of every loop in the nesting at once.

This syntax is **stable**.