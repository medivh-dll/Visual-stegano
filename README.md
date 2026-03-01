# visual_crypto

A browser-based visual cryptography tool. Split any image or text into two random-looking shares — neither reveals anything alone. Overlay both to expose the secret. No server, no key, no password. Pure math.

Part of the [covert-tools] collection alongside `steganography_studio` and `steganography_detector`.

https://medivh-dll.github.io/Visual-stegano/

---

## What is Visual Cryptography?

Visual cryptography is a technique invented by Naor & Shamir (1994) that encodes a secret image into *n* shares such that any *k* of them, when physically or digitally overlaid, reveal the secret — while any *k-1* shares are statistically indistinguishable from random noise.

This tool implements the classic **(2, 2) scheme**: 2 shares generated, both required to reveal.

### How it works

Each pixel of the secret image is expanded into a 2×2 block pattern across both shares:

| Secret pixel | Share A | Share B | Overlay (OR) |
|---|---|---|---|
| **Black** | Random 2×2 pattern | Complementary pattern | All 4 cells black |
| **White** | Random 2×2 pattern | Identical pattern | 2/4 cells black (50% grey) |

After overlaying, black secret pixels become fully black and white pixels become 50% grey — creating visible contrast that reveals the image. Neither share alone has any pattern; they are cryptographically indistinguishable from noise.

---

## Features

- **Image input** — upload any PNG/JPG; auto-resized and binarised
- **Text input** — type a secret message, rendered to canvas then encrypted
- **Adjustable pixel block size** — larger blocks make physical overlay easier
- **Overlay preview** — see the combined result instantly in-browser
- **One-click download** — both shares exported as PNG in a single click
- **Reveal tab** — upload any two shares to reconstruct the secret
- No dependencies, no server, no tracking — fully client-side

---

## Usage

### Split
1. Open `visual_cryptography.html` in any modern browser
2. Go to the **SPLIT** tab
3. Upload an image or type a secret message
4. Adjust block size (2px default; increase for physical printing)
5. Click **SPLIT SECRET**
6. Click **↓ DOWNLOAD BOTH SHARES** — `share_A_*.png` and `share_B_*.png` saved to your device
7. Distribute Share A and Share B through separate channels

### Reveal
1. Go to the **REVEAL** tab
2. Upload `share_A_*.png` and `share_B_*.png`
3. The secret appears automatically — download if needed

---

## Technical Details

| Property | Value |
|---|---|
| Scheme | (2, 2) Visual Secret Sharing |
| Pixel expansion | 2× per axis (4× total pixels) |
| Share appearance | Uniformly random — provably reveals nothing |
| Overlay operation | Bitwise OR on pixel values |
| Output format | PNG (lossless — JPEG would corrupt the LSB patterns) |
| Dependencies | None — vanilla JS + HTML Canvas API |

> **Why PNG only?** Lossy formats like JPEG recompress pixel values, corrupting the precise black/white pattern that encodes the secret. Always keep shares as PNG.

---

## Limitations

- Output image is 2× the width and height of the input (4× pixel count)
- Contrast of revealed secret is ~50% (grey vs black) — this is mathematically inherent to the scheme
- Very small or thin features may be lost during binarisation
- For physical overlay: print both shares on transparencies at the same scale and align precisely

---

## Browser Support

Any modern browser with Canvas API support. Tested on Chrome, Firefox, Safari, and Edge.

---

## References

- Naor, M. & Shamir, A. (1994). *Visual Cryptography*. EUROCRYPT 1994.
- Weir, J. & Yan, W. (2010). *A Comprehensive Study of Visual Cryptography*

---

## License

MIT
