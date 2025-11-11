# p7m-extract-macos
A lightweight command-line tool for macOS to extract content from PKCS#7 (.p7m) signed/encrypted files.

## Overview

`p7m-extract` is a simple yet powerful CLI utility that extracts the original content from PKCS#7 message files. These files are commonly used for digitally signed documents, particularly in European countries for official communications and invoices.

## Features

- **Simple extraction** - Extract .p7m files with a single command
- **Auto-detection** - Automatically detects DER and PEM formats
- **Smart naming** - Automatically generates output filenames by removing .p7m extension
- **File inspection** - View information about .p7m files before extracting
- **Zero dependencies** - Uses built-in macOS OpenSSL (no installation required)
- **Color-coded output** - Easy-to-read terminal output with color coding
- **macOS native** - Optimized for macOS including M-series chips

## Installation

### Quick Install

```bash
# Download the script
curl -O https://raw.githubusercontent.com/YOUR_USERNAME/p7m-extract/main/p7m-extract

# Make it executable
chmod +x p7m-extract

# Move to your PATH (optional but recommended)
sudo mv p7m-extract /usr/local/bin/
```

### Manual Install

1. Download the `p7m-extract` script from this repository
2. Make it executable: `chmod +x p7m-extract`
3. Move it to a directory in your PATH (e.g., `/usr/local/bin/`)

## Usage

### Basic Extraction

Extract a .p7m file (automatically generates output filename):

```bash
p7m-extract document.pdf.p7m
```

This will create `document.pdf` in the same directory.

### Specify Output File

Extract to a specific filename:

```bash
p7m-extract document.pdf.p7m my_document.pdf
```

Or use the `-o` flag:

```bash
p7m-extract -o my_document.pdf document.pdf.p7m
```

### View File Information

Display information about a .p7m file without extracting:

```bash
p7m-extract -i document.pdf.p7m
```

### Help and Version

```bash
# Show help message
p7m-extract --help

# Show version
p7m-extract --version
```

## Command Reference

```
p7m-extract [OPTIONS] <input.p7m> [output_file]

OPTIONS:
    -h, --help          Show help message
    -v, --version       Show version information
    -i, --info          Display information about the p7m file
    -o, --output FILE   Specify output file
```

## Examples

### Extract invoice
```bash
p7m-extract invoice_2024.pdf.p7m
# Creates: invoice_2024.pdf
```

### Extract with custom name
```bash
p7m-extract contract.pdf.p7m signed_contract.pdf
# Creates: signed_contract.pdf
```

### Inspect before extracting
```bash
p7m-extract -i document.pdf.p7m
# Displays file information and certificate details
```

### Batch extraction
```bash
for file in *.p7m; do
    p7m-extract "$file"
done
```

## Requirements

- macOS (tested on macOS 10.15+, including M-series chips)
- OpenSSL (pre-installed on macOS)
- Bash shell

## How It Works

`p7m-extract` uses OpenSSL's SMIME and PKCS#7 capabilities to:

1. Parse the PKCS#7 container format (DER or PEM)
2. Extract the embedded document without verifying signatures
3. Save the original file to disk

The tool attempts multiple extraction methods to ensure maximum compatibility with different .p7m formats.

## Common Use Cases

- **Italian e-invoicing** - Extract FatturaPA XML files from .p7m containers
- **Digital signatures** - Extract original documents from signed files
- **Government communications** - Process officially signed documents
- **Legal documents** - Extract contracts and agreements from signed containers

## Troubleshooting

### "Failed to extract content"

This error may occur if:
- The file is encrypted and requires a certificate/key to decrypt
- The file is corrupted
- The file is not a valid PKCS#7 format

**Solution**: Try using the `-i` flag to inspect the file structure first.

### "Input file not found"

**Solution**: Check that you've specified the correct file path. Use quotes around filenames with spaces:
```bash
p7m-extract "my document.pdf.p7m"
```

### Permission denied

**Solution**: Ensure you have read permissions for the input file and write permissions for the output directory.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Setup

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/p7m-extract.git
cd p7m-extract

# Make changes to p7m-extract

# Test your changes
./p7m-extract test_file.p7m
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Created by [Your Name]

## Acknowledgments

- Built using OpenSSL's PKCS#7 implementation
- Inspired by the need for simple .p7m file handling on macOS

## Related Projects

- [OpenSSL](https://www.openssl.org/) - The cryptographic library used by this tool
- [PKCS#7 Standard](https://tools.ietf.org/html/rfc2315) - The specification for the file format

## Support

If you encounter any issues or have questions:

- 📝 [Open an issue](https://github.com/YOUR_USERNAME/p7m-extract/issues)
- 💬 [Start a discussion](https://github.com/YOUR_USERNAME/p7m-extract/discussions)

## Changelog

### v1.0.0 (2024-11-11)
- Initial release
- Basic .p7m extraction functionality
- Support for DER and PEM formats
- File information display
- Color-coded terminal output

---

⭐ If you find this tool useful, please consider giving it a star on GitHub!
