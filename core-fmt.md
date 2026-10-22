# core:fmt Reference — Formatted I/O

`core:fmt` provides formatted input/output procedures with format verbs derived from C's `printf` but simplified.

## Package Overview

- **Collection:** `core`
- **Package:** `fmt`
- **Import path:** `core:fmt`
- **Procedures:** 82
- **Types:** 4 (`Info`, `Info_State`, `Register_User_Formatter_Error`, `User_Formatter`)

## Format Verbs

### General

| Verb | Meaning |
|------|---------|
| `%v` | Value in default format |
| `%#v` | Expanded format (newlines, indentation) |
| `%w` | Odin-syntax representation of the value |
| `%T` | Odin-syntax representation of the type |
| `%%` | Literal percent sign |
| `{{` | Literal open brace |
| `}}` | Literal close brace |
| `{:v}` | Python-like equivalent of `%v` |

### Boolean

| Verb | Meaning |
|------|---------|
| `%t` | The word `"true"` or `"false"` |

### Integer

| Verb | Meaning |
|------|---------|
| `%b` | Base 2 (binary) |
| `%c` | Character represented by Unicode code point |
| `%r` | Synonym for `%c` |
| `%o` | Base 8 (octal) |
| `%d` / `%i` | Base 10 (decimal) |
| `%z` | Base 12 (dozenal) |
| `%x` | Base 16 hex (lowercase a-f) |
| `%X` | Base 16 hex (uppercase A-F) |
| `%U` | Unicode format: `U+1234` |

### Byte Size

| Verb | Meaning |
|------|---------|
| `%m` | Bytes in best unit (e.g. `123.45mib`) |
| `%M` | Bytes in best unit (e.g. `123.45MiB`) |

### Floating-Point

| Verb | Meaning |
|------|---------|
| `%e` / `%E` | Scientific notation |
| `%f` / `%F` | Decimal point, no exponent |
| `%g` / `%G` | Synonyms for `%f` with default max precision |
| `%h` / `%H` | Hexadecimal with `0h` / `0H` prefix |

### Strings & Bytes

| Verb | Meaning |
|------|---------|
| `%s` | Uninterpreted bytes of string or slice |
| `%q` | Double-quoted string, Odin-escaped |
| `%x` / `%X` | Base 16 hex, two chars per byte |

### Pointers & Memory

| Verb | Meaning |
|------|---------|
| `%p` | Address in base 16 with `0x` prefix |

## Format Flags

| Flag | Effect |
|------|--------|
| `+` | Always print sign for numeric values |
| `-` | Left-justify (pad right) |
| `#` | Alternate format: `0b`, `0o`, `0z`, `0x` prefixes |
| ` ` | Space for elided sign |
| `0` | Pad with leading zeros |

Width is specified by a decimal number after `%`. Precision follows a period (`.2f`).

## Key Procedures

### Output to stdout
| Procedure | Description |
|-----------|-------------|
| `print(args, sep, flush)` | Default print settings to stdout |
| `printf(fmt, args, flush)` | Format string to stdout |
| `printfln(fmt, args, flush)` | Format string + newline to stdout |
| `println(args, sep, flush)` | Print with newline to stdout |

### Output to stderr
| Procedure | Description |
|-----------|-------------|
| `eprint`, `eprintf`, `eprintfln`, `eprintln` | Same as stdout variants but to stderr |

### Output to file
| Procedure | Description |
|-----------|-------------|
| `fprint(f, args, sep, flush)` | Write to `^os.File` |
| `fprintf(f, fmt, args, flush)` | Format to `^os.File` |
| `fprintfln(f, fmt, args, flush)` | Format + newline to `^os.File` |
| `fprintln(f, args, sep, flush)` | Print + newline to `^os.File` |

### Allocated string output
| Procedure | Description |
|-----------|-------------|
| `aprint(args, sep, allocator)` | Create formatted string |
| `aprintf(fmt, args, allocator, newline)` | Create formatted string with format |
| `aprintfln(fmt, args, allocator)` | Create formatted string + newline |

### Temporary allocator string output
| Procedure | Description |
|-----------|-------------|
| `tprint(args, sep)` | Temp-allocated formatted string |
| `tprintf(fmt, args, newline)` | Temp-allocated formatted string |
| `tprintfln(fmt, args)` | Temp-allocated formatted string + newline |

### Error & assertion formatting
| Procedure | Description |
|-----------|-------------|
| `panicf(fmt, args)` | Panic with formatted message |
| `assertf(cond, fmt, args)` | Assert with formatted message |
| `ensuref(cond, fmt, args)` | Ensure condition with formatted message |

## Examples

```odin
import "core:fmt"

main :: proc() {
    name := "Odin"
    version := "dev-2026-10"
    count := 42
    price := 19.99

    fmt.printfln("Welcome to %s, version %s", name, version)
    fmt.println("Count: %d, Price: %.2f", count, price)
    fmt.println("Type of version: %T", version)
    fmt.println("Hex: %x, Binary: %b", 255, 255)
    fmt.println("Pointer: %p", &count)
}
```

## Format Errors

Invalid arguments produce descriptive error strings in output:
- `%!(BAD ENUM VALUE)`
- `%!(EXTRA, ...)`
- `%!(MISSING ARGUMENT)`
- `%!(BAD WIDTH)`
- `%!(BAD PRECISION)`
- `%!(NO VERB)`
- `%!(BAD ARGUMENT NUMBER)`
- `%!(MISSING CLOSE BRACE)`

## Reference

Full API documentation: `https://pkg.odin-lang.org/core/fmt/`