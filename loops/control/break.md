<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Break | Loop Control Flow

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

``break`` stops the current loop. It behaves the same as in C.

```thrust
for var i: u32 = 0; i < 1000; i++; {
    break;
}
```

``breakall`` stops every loop in the nesting at once.

```thrust
for var i: u32 = 0; i < 1000; i++; {
    loop {
        breakall;
    }
}
```

This syntax is **stable**.