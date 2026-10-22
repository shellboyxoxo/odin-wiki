# Odin Vendor Libraries Reference

This page documents the **vendor** library collection in Odin — bindings to popular third-party libraries for graphics, windowing, audio, physics, networking, and more.

## Overview

- **Collection:** `vendor`
- **Package count:** 54 packages
- **Declaration count:** 26,903
- **License:** zlib
- **Source:** `odin-lang/Odin/vendor`

All vendor packages are shipped with the Odin compiler and can be imported directly with the `vendor:` prefix.

## Categories

### Graphics & Windowing

| Package | Description |
|---------|-------------|
| `vendor:raylib` | Simple and easy-to-use game programming library |
| `vendor:sdl3` | Simple DirectMedia Layer 3 — cross-platform multimedia library |
| `vendor:wgpu` | WebGPU bindings for graphics and compute |
| `vendor:glfw` | OpenGL, Vulkan, and windowing library |
| `vendor:vulkan` | Vulkan graphics API bindings |
| `vendor:egl` | EGL interface between rendering APIs and native windowing |
| `vendor:wasapi` | Windows Audio Session API bindings |

### Audio

| Package | Description |
|---------|-------------|
| `vendor:miniaudio` | Cross-platform audio engine (playback, capture, encoding) |
| `vendor:openal` | OpenAL — 3D audio library |
| `vendor:opusfile` | Opus audio decoding |
| `vendor:libvorbis` | Vorbis audio decoding |

### Physics

| Package | Description |
|---------|-------------|
| `vendor:box2d` | 2D physics simulation |
| `vendor:box3d` | 3D physics simulation |
| `vendor:ode` | Open Dynamics Engine |

### Networking, Crypto & Compression

| Package | Description |
|---------|-------------|
| `vendor:curl` | URL transfer library (HTTP, FTP, etc.) |
| `vendor:openssl` | Cryptography and TLS/SSL |
| `vendor:zlib` | General-purpose compression |
| `vendor:libpng` | PNG image encoding/decoding |
| `vendor:OpenEXRCore` | OpenEXR high-dynamic-range image format |

### System & Platform

| Package | Description |
|---------|-------------|
| `vendor:windows` | Windows API bindings |
| `vendor:sys/windows` | Windows system-level bindings |
| `vendor:sys/linux` | Linux system-level bindings |
| `vendor:libc-shim` | C standard library compatibility shim |

## Example Usage

### vendor:raylib — Window and Drawing

```odin
package main

import "vendor:raylib"
import "core:fmt"

main :: proc() {
    rl.InitWindow(800, 450, "Odin + raylib")
    defer rl.CloseWindow()

    for not rl.WindowShouldClose() {
        rl.BeginDrawing()
        rl.ClearBackground(rl.RAYWHITE)
        rl.DrawText("Hello from Odin!", 190, 200, 20, rl.VIOLET)
        rl.EndDrawing()
    }
}
```

Compile with: `odin run .`

### vendor:sdl3 — Event Loop

```odin
package main

import "vendor:sdl3"
import "core:fmt"

main :: proc() {
    sdl.Init(sdl.INIT_VIDEO)
    defer sdl.Quit()

    window := sdl.CreateWindow("Odin SDL3", 800, 600, sdl.WINDOW_SHOWN)
    defer sdl.DestroyWindow(window)

    event := sdl.Event{}
    running := true
    for running {
        for sdl.PollEvent(&event) != 0 {
            if event.type == sdl.EVENT_QUIT {
                running = false
            }
        }
    }
}
```

### vendor:curl — HTTP GET

```odin
package main

import "vendor:curl"
import "core:fmt"
import "core:os"

main :: proc() {
    curl.global_init(curl.INIT_ALL)
    defer curl.global_cleanup()

    easy := curl.easy_init()
    defer curl.easy_cleanup(easy)

    curl.easy_setopt(easy, curl.OPT_URL, "https://odin-lang.org/")
    code := curl.easy_perform(easy)
    fmt.println("HTTP code:", code)
}
```

## Notes

- All vendor bindings are maintained in the `odin-lang/Odin` repository under the `vendor/` directory.
- Some vendor packages have platform-specific dependencies (e.g., system libraries that must be installed separately).
- See `https://pkg.odin-lang.org/vendor/` for the full API reference of each package.