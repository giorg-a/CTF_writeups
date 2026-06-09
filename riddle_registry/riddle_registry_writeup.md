# PicoCTF — Riddle Registry
**Category:** Forensics  
**Difficulty:** Easy  

---

## Challenge
A suspicious file is provided. Find the hidden flag.

---

## Solution

### Step 1 — Download the file
```bash
wget <file_url>
```

### Step 2 — Initial recon
```bash
cat file        # output was gibberish
strings file    # nothing useful
```
Neither gave anything readable. Time to dig deeper.

### Step 3 — Check metadata with ExifTool
```bash
exiftool confidential.pdf
```
Found a base64 encoded string hidden in the metadata fields (Author/Producer).

### Step 4 — Decode the base64
```bash
nano file        # pasted the base64 string
base64 -d file   # decoded it
```

### Result
```
picoCTF{puzzl3d_m3tadata_f0und!_42440c7d}
```

---

## Key Takeaway
When `cat` and `strings` give nothing, always check file metadata with `exiftool`. Sensitive data is often hidden in plain sight inside PDF/image metadata fields.
