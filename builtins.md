# Odin Built-in Procedures Quick Reference

Odin has two categories of built-in procedures:

1. **Compiler-defined** — built into the language itself
2. **Core library-defined** — live in `base:runtime`

## Compiler-Defined Built-ins

| Procedure | Description |
|-----------|-------------|
| `len(x)` | Length of string, array, slice, dynamic array, map, etc. |
| `cap(x)` | Capacity of array, slice, dynamic array, map, etc. |
| `size_of(T)` | Size of a type in bytes |
| `align_of(T)` | Alignment of a type in bytes |
| `offset_of(T, field)` | Byte offset of a field within a struct |
| `type_of(x)` | Type of an expression |
| `typeid_of(T)` | The `typeid` of a type |
| `type_info_of(T)` | Runtime type information of a type |
| `min(a, b, ...)` | Minimum of the values |
| `max(a, b, ...)` | Maximum of the values |
| `min(T)`, `max(T)` | Smallest/largest value of a type |
| `clamp(x, lo, hi)` | Clamp value between bounds |
| `abs(x)` | Absolute value |
| `swizzle(x, indices...)` | Swizzle operations on vectors |
| `complex`, `quaternion` | Complex number / quaternion constructors |
| `real`, `imag`, `jmag`, `kmag` | Component accessors for complex/quaternion |
| `conj` | Complex conjugate |
| `expand_values(x)` | Expand struct/array into multiple values |
| `compress_values(...)` | Pack multiple values into struct/array |
| `soa_zip`, `soa_unzip` | Structure-of-Arrays operations |
| `raw_data(x)` | Raw data pointer |
| `unreachable()` | Marks unreachable code |

## Core Library Built-ins (`base:runtime`)

Memory management:

| Procedure | Description |
|-----------|-------------|
| `new(T)` | Allocate new zeroed value of type T |
| `make(T, n)` | Make slice/dynamic array of length n |
| `delete(x)` | Deallocate memory |
| `append(x, v)` | Append to dynamic array |
| `pop(x)` | Pop from dynamic array |
| `clear(x)` | Clear container |
| `resize(x, n)` | Resize dynamic array |

## Examples

```odin
import "core:fmt"
import "base:runtime"

main :: proc() {
    arr := [3]int{7, 8, 9}
    fmt.println(len(arr))           // 3
    fmt.println(size_of(int))       // 8 (on 64-bit)
    fmt.println(type_of(42))        // int
    fmt.println(min(10, 20, 5))     // 5
    fmt.println(clamp(-5, 0, 100))  // 0

    // Memory management
    ptr := new(int)                 // allocate
    ptr^ = 42
    fmt.println(ptr^)               // 42
    delete(ptr)                     // deallocate

    // expand_values / compress_values
    Vector3 :: struct { x, y, z: f32 }
    v := Vector3{1, 4, 9}
    x, y, z := expand_values(v)
    fmt.println(x, y, z)            // 1 4 9

    a := compress_values(1, 2, 3)   // [3]int{1, 2, 3}
    fmt.println(a)
}
```

## Reference

- Built-in procedures wiki: `https://github.com/odin-lang/Odin/wiki/Built-in-Procedures`
- Odin docs: `https://odin-lang.org/docs/`