<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Locals Mutation

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

A local declared with ``var`` can be reassigned. The ``=`` operator stores a new value, and ``+=`` and ``-=`` update it in place.

```thrust
var hello_world: const array[char] = "Hello World!";

hello_world = "no hello world.";

var counter: u32 = 0;
counter += 1;
counter -= 1;
```

Increment and decrement come in prefix and postfix forms.

```thrust
var i: u32 = 0;

i++;
++i;
i--;
--i;
```

This syntax is **stable**.