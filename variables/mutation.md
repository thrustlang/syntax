<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Locals Mutation

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

A local declared with ``var`` can be reassigned. The ``=`` operator stores a new value, and the compound operators update it in place with an arithmetic or bitwise operation.

- ``+=``, ``-=``, ``*=``, ``/=``, ``%=`` Arithmetic compound operators.
- ``&=``, ``|=``, ``^=``, ``<<=``, ``>>=`` Bitwise compound operators.

```thrust
var hello_world: const array[char] = "Hello World!";

hello_world = "no hello world.";

var counter: s32 = 10;
counter += 5;
counter -= 3;
counter *= 2;
counter /= 4;
counter %= 3;

var flags: u32 = 0x0F;
flags &= 0x03;
flags |= 0x10;
flags ^= 0x08;
flags <<= 1;
flags >>= 2;
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