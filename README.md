# flac-converter

A command-line tool to convert FLAC audio files to ALAC (Apple Lossless) or AAC (lossy) in M4A container format.

## Why

I have a very specific use case where I have a bunch of nested flac files I wanted to convert so I could play them in Apple Music / my iPod, and I couldn't find an out-of-the-box online utility to this for me
(the closest I could find was [this link](https://unix.stackexchange.com/questions/415477/lossless-audio-conversion-from-flac-converter-using-ffmpeg)). It seemed worth it to make this utility for myself.

The default is mp3 because it was the best sounding for the old iPod that I modded. I'm not an audiophile so I don't mind the quality; I noticed with AAC/ALAC that there was some "tearing" sounds on the iPod (not on the computer) that I didn't like. I've kept the AAC/ALAC options in case anyone was interested in that.

For transparency, most of the legwork was done by Claude Code and audited / tweaked by me. Feel free to audit the code before using it yourself.

## Features

- Convert single FLAC files to ALAC (lossless) or AAC (lossy) M4A
- Batch convert entire directories recursively
- Preserve directory structure when converting
- Specify custom output directory for batch conversions
- Preserves album artwork and metadata
- Choose between lossless (ALAC) and lossy (AAC) compression

## Requirements

- Python 3.6+
- ffmpeg

## Installation

### Quick Install (Recommended)

Install with a single command:

```bash
curl -fsSL https://raw.githubusercontent.com/jezhou/flac-converter/main/install.sh | bash
```

Or download and review the install script first:

```bash
curl -fsSL https://raw.githubusercontent.com/jezhou/flac-converter/main/install.sh -o install.sh
chmod +x install.sh
./install.sh
```

To install to a custom location (default is `/usr/local/bin`):

```bash
PREFIX=$HOME/.local ./install.sh
```

### Manual Installation

1. Ensure ffmpeg is installed:

   ```bash
   # macOS
   brew install ffmpeg

   # Ubuntu/Debian
   sudo apt-get install ffmpeg

   # Fedora
   sudo dnf install ffmpeg

   # Arch
   sudo pacman -S ffmpeg
   ```

2. Clone this repository:

   ```bash
   git clone https://github.com/jezhou/flac-converter.git
   cd flac-converter
   ```

3. Make the script executable:

   ```bash
   chmod +x flac-converter
   ```

4. Copy to your PATH:
   ```bash
   sudo cp flac-converter /usr/local/bin/
   ```

### Update

To update to the latest version:

```bash
flac-converter --update
```

Or reinstall using the install script:

```bash
curl -fsSL https://raw.githubusercontent.com/jezhou/flac-converter/main/install.sh | bash
```

### Uninstall

To remove flac-converter:

```bash
sudo rm /usr/local/bin/flac-converter
```

## Usage

### Convert a single file

Convert to ALAC (lossless, default):

```bash
flac-converter -f song.flac
```

Convert to AAC (lossy, smaller file size):

```bash
flac-converter -f song.flac --format aac
```

This will create `song.m4a` in the same directory as the input file.

### Convert all FLAC files in a directory

Convert to ALAC (default):

```bash
flac-converter -d ./music
```

Convert to AAC:

```bash
flac-converter -d ./music --format aac
```

This will recursively find all FLAC files in the `./music` directory and convert them to M4A, preserving the directory structure.

### Convert with custom output directory

```bash
flac-converter -d ./music -o ./converted
```

With AAC format:

```bash
flac-converter -d ./music -o ./converted --format aac
```

This will convert all FLAC files from `./music` and save the M4A files to `./converted`, maintaining the original directory structure.

### Check version

```bash
flac-converter --version
```

### Help

```bash
flac-converter -h
```

## Notes

- ALAC (default): Lossless compression, larger files, perfect quality
- AAC: Lossy compression at 256kbps, smaller files, very good quality
- Album artwork and metadata are preserved during conversion
- The `-o` option only works with the `-d` (directory) option

## License

MIT License
