# Version Control Details

## Version History

### v1.5.0 - StegnaVault Pro (Current Release)

**Release Date:** October 26, 2023 **Major Overhaul:** Transitioned from basic script to full "Pro" suite.

**New Features:**

- **Full Encryption:** Metadata (filename, type, size) is now fully encrypted within the payload.
- **Integrity Verification:** Added `ICRYPT_OK` verifier token to prevent decryption attempts with incorrect passwords.
- **Resizer Module:** Added nearest-neighbor upscaling (2x to 32x) to increase carrier capacity.
- **Stego-Checker:** Added header scanning to detect `<ICRYPT>` signatures.
- **Visualizer:** Added memory distribution bar chart.
- **Comparator:** Added visual slider and red-pixel difference subtraction map.
- **UI:** Complete redesign using Tailwind CSS with a "Cyber/Hacker" aesthetic.

**Bug Fixes:**

- Fixed issue where filenames were visible in the header.
- Fixed slider distortion in Comparator module.
- Improved error handling for files exceeding capacity.

### v1.0.0 - StegnaVault Initial: Project Image Steganography

[Project Link Here](https://github.com/anjalp/Project-Image-Steganography)

**Release Date:** August 1, 2020 **Initial Release:** Basic proof of concept.

**Features:**

- Basic Odd/Even Parity Encoding.
- Simple Text/File embedding.
- Single-page layout without modules.
- Python with CLI interface

## Dependencies

| Library            | Version      | Purpose                       |
| ------------------ | ------------ | ----------------------------- |
| **CryptoJS**       | 4.1.1        | AES-256 Encryption/Decryption |
| **Tailwind CSS**   | 3.x (CDN)    | Styling and Responsive Design |
| **Lucide**         | Latest       | UI Icons                      |
| **JetBrains Mono** | Google Fonts | Monospace Typography          |

## Known Issues (v1.1.0)

- **Large Files:** Very large images (4K+) may cause UI freezing during encoding/decoding due to main-thread processing. Future versions will implement Web Workers.
- **Mobile Safari:** Downloading generated images occasionally fails on older iOS versions due to blob constraints.