<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Defer

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

``defer`` schedules a block or an expression to run when the current scope ends. It is useful for cleanup, such as closing a resource before a function returns.

```thrust
fn main() s32 @public {
    defer {
        print("scope is ending\n");
    }

    return 0;
}
```

Deferred work can also be a single expression.

```thrust
defer close(handle);
```

When several ``defer`` statements exist, they run in the reverse order they were written. The last one declared runs first.

This syntax is **stable**.