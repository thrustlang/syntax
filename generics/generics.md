<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Generics

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Thrust supports generic templates that are parsed and resolved at compile time, before type checking.

- Generic parameters are declared in square brackets.
- Generic functions, structs, and type aliases are stable.
- Duplicate generic parameters are rejected, and unused generic parameters can be reported by the compiler.

### Function definition

```thrust
fn someGenerics[Some, Generics](param1: Some, param2: Generics) Generics @public {
    return param1 + param2;
} 
```

The generic parameter list is written before the function parameters.

### Function generic call type instantiation

```thrust
someGenerics[s32, s32](30, 30); // 60 
```

The generic argument list is written before the call arguments. When the compiler can infer the types from the function arguments, the generic argument list can be omitted.

```thrust
someGenerics(30, 30);
```

Generic arguments can also be partially explicit when the remaining types can be inferred.

```thrust
fn second[A, B](a: A, b: B) B {
    return b;
}

var wide: u64 = 2;
second[s32](1, wide);
```

### Structure definition

```thrust
struct Vector[T] @public {
    data: ptr[T],
    length: usize,
    capacity: usize
}
```

The generic parameter list is written before the structure attributes and body.

### Structure generic type instantiation

```thrust
var v := new Vector[s32] { 
    data: nullptr, 
    length: 0, 
    capacity: 0 
};
```

- It is generally indicated before the structure constructor body, at the type indication.

The compiler can infer generic struct arguments from constructor fields when enough type information is available.

```thrust
struct Wrapper[T] {
    value: T,
}

var w := new Wrapper { value: 10 };
```

Generic type aliases use the same bracket syntax.

```thrust
type Box[T] = ptr[T];
var boxed: Box[u64] = nullptr;
```

Imported generic symbols keep their qualified path.

```thrust
var value: module::Box[u64] = nullptr;
module::makeBox[u64](10);
```
