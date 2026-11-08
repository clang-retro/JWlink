# Changes in the fork

## Smaller programs

- **Unused data goes too.** `option eliminate` used to keep all data, and
  everything data refers to. Data COMDATs, such as C++ virtual function
  tables, `type_info` objects and jump tables, are now dropped when
  nothing that stays refers to them; a vtable no longer keeps every
  virtual function of its class, and with them most of a C++ library.
- **Aliases are followed.** A reference to an `ALIAS` name is a reference
  to the symbol it names, so the target is no longer dropped as
  unreferenced.
- **Zero-filled BSS stays out of the file.** A COMDAT in a `BSS` or
  `FAR_BSS` class that holds only zeros is uninitialized, like the segment
  it goes in, so with `-fdata-sections` BSS no longer takes room in a DOS
  `.EXE` or `.COM` file.

## 16-bit Windows

- **Only the modules that are used.** An NE file's module reference table
  listed every module an import directive named. Windows loads every
  module in the table, so with clang's `windows.lnk`, which imports the
  whole Windows 3.1 API, every program needed SHELL, COMMDLG, TOOLHELP,
  MMSYSTEM, VER and LZEXPAND, and could not load on Windows 3.0 or older.
  Now only the modules that referenced imports come from are listed.

## 32-bit OS/2 from ELF objects

- ELF `init_array`, `fini_array` and `preinit_array` sections are read,
  priority sections (`.init_array.NNN`) are folded into their base
  section, `R_386_PLT32` is a 32-bit relative fixup, and undefined weak
  symbols resolve to `__elf_weak_null`.
- An uninitialized ELF or COFF section named `.stack` is the program's
  stack, sized by `option stack=`.
- Calls to imported functions drop the `-4` that ELF keeps in the field,
  which the LX loader already accounts for, and only the DLLs that
  imports come from go in the module table.
- A weak ELF definition gives way to one already seen, without a
  "redefinition" error. C++ puts inline functions, template instances and
  vtables in every object that uses them as weak symbols; the first
  definition is used.

## Hosts

- Offset differences are sign-extended on 64-bit hosts, which fixes bad
  fixups and "exceeds 64k" errors when linking `.COM` files.
- The whole command line is read on Unix, not just its first 1024 bytes.
- An absolute weak default (a null far pointer in the far-code models)
  no longer crashes `option eliminate`.
- GNU archives' long member names (`name/` in the `//` table) are read
  without running past the end of the table.
- The automatic grouping of segments no longer reads a flag before it is
  set.
- `GccUnix.mak` builds a Windows `jwlink.exe` with the MinGW-w64 GCC.
