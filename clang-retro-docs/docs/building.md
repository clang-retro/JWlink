# Building

```sh
make -f GccUnix.mak                                        # Linux: build/jwlinkLR/jwlink
make -f GccUnix.mak CC=i686-w64-mingw32-gcc bitopts=       # Windows: build/jwlinkLR/jwlink.exe
```

The original makefiles (`Makefile` for Win32 and `OWDOS32.mak` for a
DOS-extended JWlink) use the Open Watcom toolchain. dos-sdk's
[`packaging/build-jwlink.sh`](https://github.com/clang-retro/dos-sdk/blob/main/packaging/build-jwlink.sh)
builds the copies in the toolchain package.

## CI

`.github/workflows/clang-dos-toolchain.yml` builds the clang-dos
toolchain package with each pull request's commit of JWlink and runs its
smoke test on every target, using dos-sdk's toolchain workflow and the
prebuilt LLVM tools of clang-retro/llvm.
