# Zig OpenGL binding generator

Requires Zig 0.17.0 or newer.

## Usage

`build.zig`

    const opengl = b.dependency("opengl", .{
        .api = .gl,
        .major_version = 4,
        .minor_version = 6,
        .profile = .core,
        .extensions = "",
    });

    mod.addImport("gl", opengl.module("opengl"));

`main.zig`

    makeContextCurrent();
    try gl.load(getProcAddress);
    gl.clear(gl.COLOR_BUFFER_BIT);

A default copy of `gl.xml` is provided, as the upstream repository includes
unnecessary files. To use a different copy, set the `registry` build option.

To run the generator directly:

```sh
zig build run -- src/gl.xml gl.zig gl 4.6 core
```

Arguments remain ordered as registry, output, API, version, profile, and an
optional extensions file. `zig build` installs both the generator and the
configured bindings in `zig-out`.
