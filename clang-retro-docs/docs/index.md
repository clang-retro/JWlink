---
hide:
  - navigation
---

# clang-retro JWlink

This is [JWlink](https://github.com/Baron-von-Riedesel/JWlink), Japheth's
fork of the Open Watcom linker, as the clang-retro toolchain uses it: it
links clang's OMF objects into DOS `.COM` and `.EXE` files and 16-bit
Windows and OS/2 1.x NE programs, and clang's ELF objects into 32-bit
OS/2 LX programs and DLLs. These pages describe what the fork changes.
For the linker's directives and options, see the [JWlink
manual](https://baron-von-riedesel.github.io/jwlink/html/JWlink.html).

You rarely run it yourself: clang's DOS, Windows and OS/2 drivers write
the directives and call `jwlink` (or Open Watcom's `wlink`) for you.
Pass your own directives with `-Wl,`, such as
`-Wl,option,stack=16384`, or a file of them with `-Wl,@file.lnk`.

<div class="grid cards" markdown>

-   :material-file-replace: **[Changes](changes.md)**

    ---

    Smaller programs, Windows 3.0 and older, OS/2 LX from ELF, and fixes
    for 64-bit and Unix hosts.

-   :material-hammer-wrench: **[Building](building.md)**

    ---

    Linux and Windows builds, and the CI that tests each change with the
    whole toolchain.

-   :material-view-grid-outline: **[All clang-retro projects](https://clang-retro.github.io/dos-sdk/projects/)**

    ---

    The compiler, the C library and the SDKs that JWlink links for.

</div>

## License

JWlink and the fork's changes are under the Sybase Open Watcom Public
License, as is Open Watcom.
