
## 🛠 Convert to .ttf

To generate `.ttf` files from your PNGs using FontForge:

### 🔄 Preparation:

1. **Split the PNG** into individual glyphs (e.g., with ImageMagick or a script).
2. **Name each glyph** with its Unicode value (e.g., `U+0020.png` for space, `U+0041.png` for 'A', etc.).
3. Use a script to import them into FontForge and map them correctly.

### 🧪 Script Example (Python via FontForge):

```python
import fontforge

font = fontforge.font()
font.encoding = 'UnicodeFull'

for i in range(96):
    code = ord(' ') + i
    filename = f"glyphs/U+{code:04X}.png"
    glyph = font.createChar(code)
    glyph.importOutlines(filename)

font.ascent = 32
font.descent = 0
font.em = 32
font.generate("FNTCITB.ttf")
```

---
## Python Font Conversion Script

Here’s a Python script using **FontForge** that:

* Loads a base `.ttf` file like `Roboto-Regular.ttf`
* Replaces the visible glyphs for the first 96 printable characters (starting from `' '` = U+0020) with **monospaced bitmap images** from your vertically stacked PNG font (like `FNTCITB.png`)
* Preserves metrics, kerning, and hinting from the original font (except for shape)

---

## ✅ Requirements

### Install FontForge with Python scripting:

* **Linux/macOS**:

  ```
  sudo apt install fontforge    # or `brew install fontforge` on macOS
  ```
* Confirm scripting:

  ```bash
  fontforge -script
  ```

### Make sure the following files are present:

* `FNTCITB.png` (font strip with 96 stacked glyphs)
* `Roboto-Regular.ttf` (or other base .ttf)
* `generate_font.py` (script below)

---

## 🐍 `generate_font.py`

```python
#!/usr/bin/env fontforge
import fontforge
import sys
from PIL import Image

# --- Configuration ---
SOURCE_PNG = "FNTCITB.png"
BASE_TTF = "Roboto-Regular.ttf"
OUTPUT_TTF = "FNTCITB_converted.ttf"

GLYPH_WIDTH = 24
GLYPH_HEIGHT = 32
NUM_CHARS = 96
FIRST_CHAR = ord(' ')

# --- Load PNG and slice characters ---
img = Image.open(SOURCE_PNG).convert("L")  # Grayscale
png_width, png_height = img.size
assert png_width == GLYPH_WIDTH, "PNG width must match GLYPH_WIDTH"
assert png_height == GLYPH_HEIGHT * NUM_CHARS, "PNG height must be GLYPH_HEIGHT * 96"

# --- Load base font ---
font = fontforge.open(BASE_TTF)
font.fontname = "FNTCITB_Converted"
font.fullname = "FNTCITB Converted"
font.familyname = "FNTCITB"

# --- Replace 96 glyphs ---
for i in range(NUM_CHARS):
    codepoint = FIRST_CHAR + i
    glyph_img = img.crop((0, i * GLYPH_HEIGHT, GLYPH_WIDTH, (i + 1) * GLYPH_HEIGHT))
    
    # Save temporary image file
    tmpfile = f"/tmp/glyph_{codepoint}.png"
    glyph_img.save(tmpfile)

    # Replace glyph
    glyph = font.createChar(codepoint)
    glyph.clear()
    glyph.importOutlines(tmpfile)
    glyph.width = GLYPH_WIDTH

print(f"Writing font to {OUTPUT_TTF} ...")
font.generate(OUTPUT_TTF)
print("Done.")
```

---

## 🧪 To Run:

```bash
fontforge -script generate_font.py
```

> This will produce: `FNTCITB_converted.ttf` — a valid TrueType font using your custom bitmaps overlaid on a Roboto metrics base.

---

## 📌 Notes:

* You can change `SOURCE_PNG`, `GLYPH_WIDTH`, and `GLYPH_HEIGHT` to handle any of your `FNT*.png` fonts.
* This approach **preserves line spacing, kerning tables**, and **hinting behavior** from the original `.ttf`, while overriding just the glyph visuals.

#

## Batch processing 

Here's a **FontForge Python script** that automatically processes **all `FNT*.png` font strips** in the current directory and generates `.ttf` files by:

* Loading **each `FNT*.png`** vertical glyph strip
* Using **`Roboto-Regular.ttf`** as the source for font metrics
* Slicing each strip into **96 glyphs** starting from ASCII space `' '` (U+0020)
* Saving the output as **`<input>.ttf`**, e.g., `FNTCITB.ttf`

---

## 🐍 `batch_generate_fonts.py`

```python
#!/usr/bin/env fontforge
import fontforge
import glob
import os
from PIL import Image

# --- Configuration ---
BASE_TTF = "Roboto-Regular.ttf"  # This must exist in the working directory
GLYPH_COUNT = 96
FIRST_CHAR = ord(' ')  # Start at space character (U+0020)

# --- Load PNG-based bitmap font strips ---
for png_file in glob.glob("FNT*.png"):
    print(f"\nProcessing {png_file}...")

    # Load image and check size
    img = Image.open(png_file).convert("L")  # grayscale only
    width, height = img.size
    glyph_width = width
    glyph_height = height // GLYPH_COUNT

    assert height % GLYPH_COUNT == 0, f"Image height must be divisible by {GLYPH_COUNT}"

    # Create new font from base
    font = fontforge.open(BASE_TTF)
    font.fontname = os.path.splitext(png_file)[0]
    font.familyname = font.fontname
    font.fullname = font.fontname

    # Replace each glyph
    for i in range(GLYPH_COUNT):
        codepoint = FIRST_CHAR + i
        top = i * glyph_height
        bottom = (i + 1) * glyph_height
        glyph_img = img.crop((0, top, glyph_width, bottom))

        # Save to temp file
        tmp_path = f"/tmp/{font.fontname}_{codepoint}.png"
        glyph_img.save(tmp_path)

        # Import into glyph
        glyph = font.createChar(codepoint)
        glyph.clear()
        glyph.importOutlines(tmp_path)
        glyph.width = glyph_width

    # Output .ttf
    output_ttf = f"{font.fontname}.ttf"
    print(f"Saving to {output_ttf}...")
    font.generate(output_ttf)
    print("Done.")

print("\nAll fonts processed.")
```

---

## ✅ To Use:

1. **Place in your working directory:**

   * All your `FNT*.png` font strips
   * `Roboto-Regular.ttf` as the base

2. **Run with FontForge:**

   ```bash
   fontforge -script batch_generate_fonts.py
   ```

---

## 💡 Notes:

* It assumes glyphs are stacked vertically and each glyph is **full PNG width** and `height / 96`.
* If you're using **color glyphs** (RGBA), change `.convert("L")` to `.convert("RGBA")` and tweak `importOutlines()` as needed (it works best with monochrome glyphs).
* Output fonts are drop-in compatible with **SDL\_ttf**, **stb\_truetype**, or any other TTF consumer.

---

## Convert Azaria font files to svg images:

* Takes a vertically stacked PNG font strip like your `FNTCITB.png`
* Extracts each of the 96 glyphs starting from `' '` (space, U+0020)
* Saves each character as an individual **SVG file** (monochrome)

> This is ideal if you want to use these images in FontForge or any vector font-building tool.

---

## 🐍 `png_to_svg_strip.py`

```python
import os
from PIL import Image
import numpy as np

# --- Configuration ---
SOURCE_PNG = "FNTCITB.png"  # input strip image
OUTPUT_DIR = "glyphs_svg"   # folder to save SVGs
GLYPH_COUNT = 96
START_CODEPOINT = ord(' ')  # U+0020
SVG_WIDTH = 1000            # canvas width in SVG units
SVG_HEIGHT = 1000           # canvas height in SVG units

# --- Load PNG strip ---
img = Image.open(SOURCE_PNG).convert("L")  # Grayscale
img_width, img_height = img.size
glyph_height = img_height // GLYPH_COUNT
glyph_width = img_width

# --- Ensure output directory exists ---
os.makedirs(OUTPUT_DIR, exist_ok=True)

# --- Generate SVGs ---
for i in range(GLYPH_COUNT):
    codepoint = START_CODEPOINT + i
    char = chr(codepoint)
    glyph_img = img.crop((0, i * glyph_height, glyph_width, (i + 1) * glyph_height))
    pixels = np.array(glyph_img)

    svg_file = os.path.join(OUTPUT_DIR, f"U+{codepoint:04X}_{char}.svg")
    with open(svg_file, "w") as f:
        f.write(f'<svg xmlns="http://www.w3.org/2000/svg" '
                f'width="{SVG_WIDTH}" height="{SVG_HEIGHT}" '
                f'viewBox="0 0 {glyph_width} {glyph_height}">\n')

        for y in range(glyph_height):
            for x in range(glyph_width):
                v = pixels[y][x]
                if v > 0:
                    alpha = v / 255.0
                    f.write(f'<rect x="{x}" y="{y}" width="1" height="1" '
                            f'fill="black" fill-opacity="{alpha:.3f}" />\n')

        f.write('</svg>\n')

print(f"Exported {GLYPH_COUNT} glyphs to {OUTPUT_DIR}/ as individual SVG files.")
```

---

## 🔧 Output

* SVGs named like `U+0041_A.svg`, `U+0030_0.svg`, etc.
* Compatible with tools like **FontForge** for vector font assembly
* Each SVG uses `<rect>` for each visible pixel with correct alpha (antialiased if source is soft)

---

Excellent — for clean, vectorized paths from bitmap font images, the standard approach is:

> **Bitmap → SVG path tracing → SVG font or .ttf**

We’ll use **[Potrace](http://potrace.sourceforge.net/)** to do the heavy lifting. It converts a black-and-white bitmap into smooth vector paths (like those found in `.ttf` or `.svg` fonts).

---

## ✅ Final Output Goal

* Take your `FNT*.png` strip
* Slice it into 96 monochrome character images
* Convert each to a clean **single-path SVG** using `potrace`

---

## 🧰 Requirements

1. **Install Potrace**

### Linux/macOS:

```bash
sudo apt install potrace        # Debian/Ubuntu
brew install potrace           # macOS (Homebrew)
```

### Python packages:

```bash
pip install pillow numpy
```

---

## 🐍 `png_strip_to_vector_svg.py`

```python
import os
import subprocess
from PIL import Image

# --- Configuration ---
SOURCE_PNG = "FNTCITB.png"
OUTPUT_DIR = "vector_svg"
TMP_DIR = "/tmp/font_convert"
GLYPH_COUNT = 96
START_CODEPOINT = ord(' ')
BW_THRESHOLD = 128  # pixels > this become white; otherwise black

# --- Prepare workspace ---
os.makedirs(OUTPUT_DIR, exist_ok=True)
os.makedirs(TMP_DIR, exist_ok=True)

# --- Load and slice PNG strip ---
img = Image.open(SOURCE_PNG).convert("L")
img_width, img_height = img.size
glyph_height = img_height // GLYPH_COUNT
glyph_width = img_width

for i in range(GLYPH_COUNT):
    codepoint = START_CODEPOINT + i
    char = chr(codepoint)
    filename_base = f"U+{codepoint:04X}_{char}"

    # Slice out the glyph
    glyph_img = img.crop((0, i * glyph_height, glyph_width, (i + 1) * glyph_height))
    
    # Convert to black & white PBM (required for potrace)
    bw_img = glyph_img.point(lambda p: 0 if p < BW_THRESHOLD else 255, mode='1')
    pbm_path = os.path.join(TMP_DIR, f"{filename_base}.pbm")
    bw_img.save(pbm_path, format='PBM')

    # Call potrace to generate an SVG path
    svg_path = os.path.join(OUTPUT_DIR, f"{filename_base}.svg")
    subprocess.run([
        "potrace", pbm_path,
        "--svg", "-o", svg_path,
        "--unit=1", "--flat", "--opaque"
    ])

print(f"✅ Vectorized SVGs saved to {OUTPUT_DIR}/")
```

---

## 📁 Output

* SVGs like `U+0041_A.svg` with clean `<path>` elements
* Scalable, editable, and importable into FontForge or Inkscape

---

## 📌 Notes

* Potrace generates **smooth Bézier curves** — great for `.ttf` generation.
* You can adjust the `--turdsize` or `--alphamax` parameters to refine the trace.
* If needed, you can modify `--unit` and `--scale` to align glyph sizes to em boxes for font creation.

---

## Script that assembles these vector SVGs into a real `.ttf` using FontForge


Now that you have clean SVG files for each glyph (e.g., `U+0041_A.svg`), here's the final script that:

---

## ✅ Assembles Your Vectorized SVGs into a `.ttf` Font Using FontForge

### 🧩 Assumptions:

* You have 96 SVGs named like: `U+0020_ .svg`, `U+0041_A.svg`, etc.
* All SVGs are in a folder (e.g., `vector_svg/`)
* You want to build a `.ttf` using those paths and standard font metrics

---

## 🐍 `svg_to_ttf_fontforge.py` (FontForge Python Script)

```python
#!/usr/bin/env fontforge
import fontforge
import os
import re

# --- Configuration ---
GLYPH_DIR = "vector_svg"
OUTPUT_TTF = "CustomBitmapFont.ttf"
FONT_NAME = "CustomBitmapFont"
ASCENT = 32
EM_SIZE = 64

# --- Setup font object ---
font = fontforge.font()
font.encoding = 'UnicodeFull'
font.fontname = FONT_NAME
font.familyname = FONT_NAME
font.fullname = FONT_NAME
font.ascent = ASCENT
font.descent = 0
font.em = EM_SIZE

# --- Load and import glyphs ---
for fname in sorted(os.listdir(GLYPH_DIR)):
    match = re.match(r"U\+([0-9A-Fa-f]{4})_.*\.svg", fname)
    if not match:
        continue
    codepoint = int(match.group(1), 16)
    glyph_path = os.path.join(GLYPH_DIR, fname)

    print(f"Importing U+{codepoint:04X} from {fname}...")
    glyph = font.createChar(codepoint)
    glyph.clear()
    glyph.importOutlines(glyph_path)
    glyph.width = EM_SIZE  # Monospaced advance

# --- Generate TTF font ---
print(f"Saving font to {OUTPUT_TTF}...")
font.generate(OUTPUT_TTF)
print("✅ Font generation complete.")
```

---

## 📁 File Layout Example

```
your_project/
├── vector_svg/
│   ├── U+0020_ .svg
│   ├── U+0041_A.svg
│   └── U+005A_Z.svg
├── svg_to_ttf_fontforge.py
```

---

## 🚀 Run It

```bash
fontforge -script svg_to_ttf_fontforge.py
```

---

## 🧪 Output

* `CustomBitmapFont.ttf` — a real, installable TrueType font
* Compatible with SDL\_ttf, stb\_truetype, system renderers, and even MS Word

---

## 🛠 Optional Enhancements

* Vary `glyph.width` per character for proportional fonts
* Add kerning and hinting
* Set baseline alignment and vertical metrics explicitly

---

Let me know if you'd like to automatically:

* Add all your `FNT*.png` fonts into a batch `.ttf` builder
* Generate `.woff` or `.otf`
* Export a `.fnt` bitmap metadata file alongside the `.ttf`
