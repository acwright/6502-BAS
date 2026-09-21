6502-BAS
========

BASIC program listings for the [AC6502](https://github.com/acwright/6502-ACE) family of computer systems.

Each listing lives in its own directory as a `.txt` source file and can be
tokenized into a `.prg` and packaged onto a CompactFlash disk image for the
system's BASIC interpreter.

> 📖 **Guide:** [AC6502 Documentation](https://acwright.github.io/6502-DOCS/) — the user's and programmer's guide for the whole family.
> The dialect these listings are written in is taught in [the BASIC guide](https://acwright.github.io/6502-DOCS/basic/).

## What this repository is for

This is where small BASIC programs for the AC6502 family live: demos, samples,
scratchpads, tests, and listings typed in from a book to see whether they run.
Each one is a directory with its own `.txt` source, its own Makefile and its
own README, and the top-level `make` builds all of them.

Anything larger gets a repository of its own. A game or an application has
releases, issues and documentation of its own, and none of that fits in a
directory next to a thirty-line listing.

The same idea in the other two languages:

- [6502-ASM](https://github.com/acwright/6502-ASM) — assembly programs
- [6502-C](https://github.com/acwright/6502-C) — C programs, built with cc65

Those two are also where a listing goes when the interpreter turns out to be
too slow for it, and neither starts from an empty directory. There are three
templates for that:

| Template | What it makes |
|---|---|
| [6502-PRG](https://github.com/acwright/6502-PRG) | A `.prg` — a program in RAM, loaded and started from BASIC with `RUN` |
| [6502-CRT](https://github.com/acwright/6502-CRT) | A `.crt` — a cartridge ROM, or a banked Flash Cart |
| [6502-BIN](https://github.com/acwright/6502-BIN) | A `.bin` — raw machine code with no BASIC stub, entered at `$0800` |

## Building Programs

Each listing directory contains its own Makefile. To build a listing, navigate to its directory and use `make`.

### Prerequisites

#### bastok

Install from NPM:
```bash
npm install -g bastok
```

The `bastok` tool tokenizes BASIC source text into the `.prg` program images the interpreter loads and runs, and can detokenize them back to text.

For more information, see the [bastok project](https://github.com/acwright/bastok).

#### cffs

Install from NPM:
```bash
npm install -g cffs-image-tool
```

The `cffs` tool is used to create CompactFlash disk images and add files to them. It's required for the `make cf` target.

For more information, see the [cffs project](https://github.com/acwright/cffs).

#### 6502 CLI

Installed via the [6502-EMULATOR](https://github.com/acwright/6502-EMULATOR) app's Settings → Command Line → Install. Required for the `make run` target.

### Available Targets

- `make` or `make all` - Tokenize the listing and build a CompactFlash image containing it
- `make build` - Tokenize the listing into a `.prg`
- `make view` - Display hexdump of the tokenized `.prg`
- `make cf` - Create a CompactFlash image and add the `.prg` to it
- `make run` - Launch the emulator app with the tokenized listing loaded
- `make clean` - Remove build artifacts

### Example

```bash
cd RKPAPSC
make        # Tokenize the listing and build the CF image
make view   # View the hexdump
make run    # Launch the emulator
```

## Usage

The `.txt` source in each directory is a plain-text BASIC listing and can also be typed directly into the interpreter by hand if you'd rather not build it. Program listings load at `$0800`, matching the system's `PROGRAM_START`.

## Contributing

A listing here is a directory: the top-level Makefile picks up anything with a
`Makefile` in it, so adding one is the whole of the mechanism.

1. **Name the directory after the program**, in the upper case the machine
   shows it in: `RKPAPSC`. The `.txt` source and the `.prg` it tokenizes to
   take the same name.
2. **Keep the name to 8.3.** CompactFlash directory entries are 8.3, so the
   name that goes onto the image is at most eight characters plus `.PRG`. The
   Makefile keeps it in its own `EIGHTTHREE` variable, which is there for the
   case where the directory name is longer and the on-disk name has to be an
   abbreviation of it.
3. **Copy the nearest existing Makefile** and change those two names. Every
   directory answers `make`, `make build`, `make view`, `make cf`, `make run`
   and `make clean`.
4. **Write the listing the way you would type it in** — line numbers, the
   dialect's own keywords, plain text. `bastok` tokenizes it, and anything it
   refuses is a line the interpreter would have refused too. The
   [BASIC guide](https://acwright.github.io/6502-DOCS/basic/) is what the
   dialect actually is.
5. **Write a README for the directory** — what the program does, where it came
   from if you did not write it, and anything it needs beyond a bare machine.
   See [RKPAPSC](RKPAPSC/README.md) for the shape.
6. **Commit the `.txt` and the `.prg`**, so a reader can see both without
   installing anything. The CompactFlash image is in `.gitignore`; `make cf`
   rebuilds it.

Then open a pull request. If the program turned into something with a life of
its own while you were writing it, give it a repository of its own instead and
[add it to the software list](https://acwright.github.io/6502-DOCS/software/)
on the documentation site.

## Related

- [6502-ACE](https://github.com/acwright/6502-ACE) — the hardware, and the index of the whole family
- [6502-BIOS](https://github.com/acwright/6502-BIOS) — the BASIC dialect these listings are written in
- [6502-EMULATOR](https://github.com/acwright/6502-EMULATOR) — run a listing without hardware (`make run`)
- [6502-ASM](https://github.com/acwright/6502-ASM) — the same kind of collection for assembly language
- [6502-C](https://github.com/acwright/6502-C) — the same kind of collection for C, built with cc65
- [6502-PRG](https://github.com/acwright/6502-PRG) / [6502-CRT](https://github.com/acwright/6502-CRT) / [6502-BIN](https://github.com/acwright/6502-BIN) — templates for starting a program, a cartridge or a raw binary
- [bastok](https://github.com/acwright/bastok) / [cffs](https://github.com/acwright/cffs) — the tools behind `make build` and `make cf`
- [6502-DOCS](https://github.com/acwright/6502-DOCS) — the documentation site: the BASIC guide and the printable reference cards

## License

MIT License — see [LICENSE](LICENSE).
