<img src= "https://github.com/thrustlang/.github/blob/main/assets/logos/new%20logo/thrustlang-logo-banner-text-italic.png" alt= "logo" style= "width: 80%; height: 80%;"></img>

# Generics

<img src= "https://github.com/thrustlang/.github/blob/main/assets/standard-text-separator.png" alt= "standard-separator" style= "width: 1hv;"> </img>

Thrust is capable on the write time of this, utilize and define generics templates, which can be used easily for dynamic typing on compile time.

- All generics templates are parsed and resolved in compile time. Before typechecking.

### Function definition

```thrust
fn someGenerics [Some, Generics] (param1: Some, param2: Generics) Generics @public {
    return param1 + param2;
} 
```

- It is generally declared before the construction of the function parameters.

### Function generic call type instantiation

```thrust
someGenerics[s32, s32](30, 30); // 60 
```

- It is generally declared before the construction of the function arguments in the callee.

### Structure definition

```thrust
struct Vector [T] @public {
    data: ptr[T],
    length: usize,
    capacity: usize
}
```

- It is generally declared before the structure attributes or body construction.

### Structure generic type instantiation

```thrust
var v := new Vector[s32] { 
    data: nullptr, 
    length: 0, 
    capacity: 0 
};
```

- It is generally indicated before the structure constructor body, at the type indication.
