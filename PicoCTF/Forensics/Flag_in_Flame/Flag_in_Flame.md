# PicoCTF — Flag in Flame

**Category:** Forensics
**Difficulty:** Easy/Medium

## Challenge

Given a `logs.txt` file containing a large block of what looked like base64-encoded text.

## Approach

### 1. Decode the base64
Ran the file through base64 decoding to see what was actually inside:
```bash
base64 -d logs.txt > output.bin
```

### 2. Identify the file type
Used `exiftool` on the decoded output to figure out what kind of data it was, since base64 blobs are often binary files in disguise:
```bash
exiftool output.bin
```
Output confirmed it was a **PNG image** (896x1152, RGB, 8-bit depth).

### 3. Rename and inspect
Renamed the file to match its actual type so image tools would handle it correctly:
```bash
mv output.bin output.png
```

### 4. Try OCR first
Ran `tesseract` to check for any text embedded visually in the image:
```bash
tesseract output.png stdout
```
This returned mostly garbled/noisy text, but one line stood out as clean, structured hex:
```
7069636F4354467B666F72656E736963735F 616E616C797369735F69735F61 6D617A696E675F35646161346132667D
```

### 5. Confirm visually
Opened the image directly to double check the hex string was visible in the picture itself:
```bash
xdg-open output.png
```

### 6. Decode the hex string
Stripped the spaces and decoded the hex to ASCII:
```bash
echo "7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35646161346132667D" | xxd -r -p
```

### Flag
```
picoCTF{forensics_analysis_is_amazing_5daa4a2f}
```

## Takeaway

Multi-layer decode chain: **base64 → PNG → hex string embedded as visible text in the image → ASCII**. Good reminder to always run `file`/`exiftool` on decoded output before assuming what it is, and that OCR is worth trying even when an image looks noisy — the actual payload can be sitting right next to visual noise.
