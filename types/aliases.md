<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Type Aliases

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

A type alias gives a name to an existing type. It does not create a new type, it just makes the old one shorter to write.

```thrust
type Depth @public = u16;
type Pair = array[u32; 2];
type Identity[T] = T;
```

Aliases can be exported to other modules with ``@public``, and then imported and used as any other type. Type aliases can be declared at the top level or inside a function body.

```thrust
// other.thrust
type Depth @public = u16;

// main.thrust
import "other.thrust";

fn main() s32 @public {
    var depth: other::Depth = 7;
    return depth as s32;
}
```

Aliases can be generic. Type arguments are written in brackets at the use site.

```thrust
type Box[T] = ptr[T];

fn main() s32 @public {
    var p: Box[u64] = nullptr;
    return 0;
}
```

This syntax is **stable**.
