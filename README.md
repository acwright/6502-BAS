6502-BAS
========

BASIC program listings for the [A.C. Wright 6502](https://github.com/acwright/6502-ACE) family of computer systems.

Each listing lives in its own directory as a `.txt` source file and can be
tokenized into a `.prg` and packaged onto a CompactFlash disk image for the
system's BASIC interpreter.

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

### Available Targets

- `make` or `make all` - Tokenize the listing and build a CompactFlash image containing it
- `make build` - Tokenize the listing into a `.prg`
- `make view` - Display hexdump of the tokenized `.prg`
- `make cf` - Create a CompactFlash image and add the `.prg` to it
- `make clean` - Remove build artifacts

### Example

```bash
cd RKPAPSC
make        # Tokenize the listing and build the CF image
make view   # View the hexdump
```

## Usage

The `.txt` source in each directory is a plain-text BASIC listing and can also be typed directly into the interpreter by hand if you'd rather not build it. Program listings load at `$0800`, matching the system's `PROGRAM_START`.
