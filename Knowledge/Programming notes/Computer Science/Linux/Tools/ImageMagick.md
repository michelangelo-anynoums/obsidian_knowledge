# 🖼️ ImageMagick — Image manipulation in Linux

> A powerful command-line tool to create, convert, resize, edit and inspect images directly from the terminal.

## 📦 Installation


```bash
sudo apt install imagemagick
```

Check installation:

```bash
magick -version
```

## 🔍 Basic commands

### 📋 Get image information

```bash
identify image.jpg
identify -verbose image.jpg
```

### 🔄 Convert image formats

```bash
magick image.jpg image.png
magick image.png image.webp
```

### 📐 Resize images


```bash
magick image.jpg -resize 800x600 resized.jpg
```

Keep aspect ratio:

```bash
magick image.jpg -resize 800x output.jpg
```

Force exact dimensions:

```bash
magick image.jpg -resize 800x600! output.jpg
```

### ✂️ Crop images


```bash
magick image.jpg -crop 500x300+10+20 cropped.jpg
```

Format: `WIDTHxHEIGHT+X+Y`

### 🔃 Rotate images

```bash
magick image.jpg -rotate 90 rotated.jpg
```

### 🌗 Adjust brightness and contrast

```bash
magick image.jpg -brightness-contrast 10x15 output.jpg
```

### ⚫ Convert to grayscale


```bash
magick image.jpg -colorspace Gray gray.jpg
```

### 🗜️ Compress images

```bash
magick image.jpg -quality 75 compressed.jpg
```

Lower quality = smaller file size.

### 📝 Add text to an image

```bash
magick image.jpg \
  -gravity South \
  -pointsize 30 \
  -fill white \
  -annotate +0+20 "Hello Linux" \
  output.jpg
```

### 🧩 Combine images

```bash
magick montage img1.jpg img2.jpg img3.jpg \
  -tile 3x1 -geometry 200x200+5+5 \
  montage.jpg
```

### 📄 Create a GIF

```bash
magick -delay 100 frame*.jpg animation.gif
```

### 📑 Convert PDF pages to images

```bash
magick document.pdf page.png
```

_Note: PDF conversion may require Ghostscript and appropriate security policy permissions._

## ⚡ Useful operators

|Operator|Purpose|
|---|---|
|`-resize`|Resize|
|`-crop`|Crop|
|`-rotate`|Rotate|
|`-flip`|Flip vertically|
|`-flop`|Flip horizontally|
|`-quality`|Compression quality|
|`-blur`|Blur|
|`-negate`|Invert colors|
|`-sharpen`|Sharpen|
|`-strip`|Remove metadata|

## 🚀 Batch processing

Resize every JPG in a folder:

```bash
mkdir resized

for img in *.jpg; do
    magick "$img" -resize 800x "resized/$img"
done
```

Convert all PNG files to JPG:

```bash
mogrify -format jpg *.png
```

⚠️ `mogrify` modifies original files when processing in place. Use copies if you need to preserve them.

## 💡 Remember

- `magick` → Create and manipulate images.
- `identify` → Inspect image properties.
- `mogrify` → Modify multiple images.
- `montage` → Combine images.

**ImageMagick = Image editing power, straight from the Linux terminal.** 🐧

---
