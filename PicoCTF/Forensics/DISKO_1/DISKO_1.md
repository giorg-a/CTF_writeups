# PicoCTF — Disko 1

**Category:** Forensics
**Difficulty:** Easy

## Challenge

Given a large disk image file, `disko-1.dd.gz`.

## Approach

### 1. Decompress the disk image
The file was gzip-compressed, so unzipped it first:
```bash
gunzip disko-1.dd.gz
```
This left a raw disk image, `disko-1.dd`.

### 2. Skip mounting, go straight for strings
Rather than mounting the disk image as a filesystem and manually browsing through directories/files, went straight for the raw text inside the binary:
```bash
strings disko-1.dd | grep pico
```
`strings` pulls every printable character sequence out of the raw disk data regardless of filesystem structure, and grepping for `pico` filtered straight down to the flag's prefix.

### Flag
```
picoCTF{1t5_ju5t_4_5tr1n9_c63b02ef}
```

## Takeaway

Not every forensics challenge needs the "proper" approach (mounting the image, browsing the filesystem, using tools like Autopsy/Sleuthkit). When the goal is just finding a flag string, `strings | grep` on the raw disk image is often the fastest path — mounting and manual exploration is more useful when you actually need file structure, metadata, or deleted-file recovery.
