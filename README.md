# StegnaVault Pro 🛡️

**Advanced Browser-Based Steganography Suite via Images**

StegnaVault Pro is a client-side web application that combines military-grade encryption (AES) with image steganography to hide files inside standard images. Unlike simple LSB tools, StegnaVault Pro uses a custom parity-based encoding algorithm spread across pixel blocks, ensuring data integrity and minimal visual distortion.

## 🚀 Features

### 1. FCrypt (File Encryption & Hiding)

The core module that encrypts files and embeds them into a "carrier" image.

- **Full Privacy:** Encrypts filenames, file types, and sizes. Even if the steganography is detected, the metadata remains hidden.
- **Capacity Calculation:** Automatically calculates max file size based on image resolution.

### 2. Decrypt (Extraction)

Retrieves hidden data from stego-images.

- **Integrity Check:** Uses a hidden "Verifier Token" to instantly reject incorrect passwords without generating corrupted files.
- **Auto-Restoration:** Restores the original filename and file type automatically upon successful decryption.

### 3. Stego-Checker

A diagnostic tool to analyze images.

- **Header Detection:** Scans for the proprietary `<ICRYPT>` signature.
- **Privacy Safe:** Confirms the presence of hidden data without revealing what it is (since headers are now encrypted).

### 4. Resizer (Capacity Expander)

Increases the storage capacity of small images using specific algorithms.

- **Nearest Neighbor:** Upscales images without blurring, preserving sharp edges ideal for pixel manipulation.
- **Scale:** Supports up to 32x upscaling for massive storage potential.

### 5. Visualizer

A graphical representation of the hidden data structure.

- Shows the memory distribution (Header, Encrypted Payload, Free Space).

### 6. Comparator

A forensic tool to compare Original vs. Stego images.

- **Slider View:** Interactive swipe to see visual differences.
- **Difference Map:** Subtracts pixel values to highlight modified bits in red.

## 🧠 How It Works

### Steganography Algorithm: The 3-Pixel Block Method

Instead of the standard Least Significant Bit (LSB) method which can be fragile, StegnaVault Pro uses a custom **Parity Encoding Scheme** distributed over 3-pixel blocks.

1. **The Grid:** The image is treated as a linear array of pixels.
2. **The Block:** We group every **3 pixels** together.
   - 3 Pixels = 9 Color Channels (R, G, B x 3).
3. **The Payload:** Each block stores **1 Byte (8 bits)** of data + **1 Parity Bit**.
4. **Encoding Logic:**
   - The algorithm reads the bit (0 or 1).
   - It adjusts the channel value to be **Even** (for 0) or **Odd** (for 1).
   - *Example:* If we need to store a `1` (Odd) and the Red channel is `200` (Even), it changes to `201`.
   - This creates a minimal change (+/- 1 value) invisible to the human eye.

**Capacity Formula:**

$$\text{Capacity (Bytes)} \approx \frac{\text{Width} \times \text{Height}}{3}$$

### Security Architecture

StegnaVault Pro employs a "Wrap-then-Encrypt" strategy using `CryptoJS` (AES).

#### 1. The Secure Object

Before encryption, the file is wrapped in a JSON structure:

```
{
  "verifier": "ICRYPT_OK",
  "meta": {
    "n": "secret_plans.pdf",
    "t": "application/pdf",
    "s": 10240
  },
  "data": "base64_encoded_string..."
}
```

#### 2. The Payload Structure

The object above is stringified and AES-encrypted. It is then sandwiched between magic signatures: `<ICRYPT>` + `[AES ENCRYPTED BLOB]` + `</ICRYPT>`

#### 3. The Verifier Token

When decrypting, the app first looks for the `verifier` key: `"ICRYPT_OK"`.

- **If Pass is Correct:** The token is found, and the file is extracted.
- **If Pass is Wrong:** The decryption produces garbage, the token is missing, and the app throws an "Integrity Check Failed" error.

## 🛠️ Tools & Tech Stack

- **Core:** HTML5, JavaScript (ES6+).
- **UI Framework:** Tailwind CSS (via CDN).
- **Cryptography:** `crypto-js` (AES implementation).
- **Icons:** Lucide Icons.
- **Font:** JetBrains Mono (Google Fonts).

## 💡 Tips & Tricks

1. **Image Formats:**
   - Always save/share the output as **PNG**.
   - **Never** convert the output to JPG/JPEG. JPEG compression destroys the specific odd/even pixel values, corrupting the data.
2. **Maximizing Capacity:**
   - If your image is too small for your file, use the **Resizer** tab.
   - Select **"Nearest Neighbor"** for the cleanest upscale.
   - A 1920x1080 image can hold approx **690 KB**.
   - Upscaling by 2x quadruples the capacity.
3. **Password Safety:**
   - Because the filename and type are inside the encrypted blob, if you lose the password, **you lose the file type information too**. You won't know if the hidden file was a PDF or an Image.

## 🔮 Future Directions

The following features are planned for future iterations of StegnaVault:

1. **Incorporating JPEG Files:** Developing DCT (Discrete Cosine Transform) modification algorithms to allow data hiding that survives JPEG compression.
2. **Audio Steganography:** Extending the parity encoding logic to WAV audio samples or MP3 frames to hide data in sound files.
3. **Video Steganography:** Hiding data across frames in video files, utilizing the vast storage capacity of video containers.

## 📦 Installation

StegnaVault Pro is a single-file application (`stegnaVault_pro.html`).

1. Download the `.html` file.
2. Open it in any modern web browser (Chrome, Firefox, Edge, Safari).
3. No server or internet connection is required (it runs entirely offline).

## 📦 Vrsion Control Detsils: 
version Details.md

## ⚠️ Disclaimer

This tool is for educational and privacy-protection purposes. Users are responsible for complying with local laws regarding encryption and data hiding.
