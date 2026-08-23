<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Conditionals

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

The ``if`` statement runs a block when a condition is true. It can be chained with ``elif`` and given a fallback with ``else``.

```thrust
if value > 10 {
    // runs when value > 10
} elif value > 5 {
    // runs when value > 5 and the first check failed
} else {
    // runs in any other case
}
```

The condition does not need parentheses. The form ``else if`` works the same as ``elif``.

```thrust
if result >= 0 {
    print("found\n");
} else {
    print("not found\n");
}
```

This syntax is **stable**.