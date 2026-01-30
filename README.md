# Wine Patches for Clip Studio Paint Video Export

Adds H.264 video encoding support to Wine so Clip Studio Paint can export animations and timelapses.

## Quick Install

**Pre-built DLLs** (in `release/` folder):
```bash
# System Wine (requires root)
sudo cp release/x86_64-windows/*.dll /usr/lib/wine/x86_64-windows/
sudo cp release/x86_64-unix/*.so /usr/lib/wine/x86_64-unix/

# For Bottles - copy to your bottle's system32
cp release/x86_64-windows/*.dll ~/.local/share/bottles/bottles/YOUR_BOTTLE_NAME/drive_c/windows/system32/
```

**Or apply patch to Wine source:**
```bash
cd wine-source
patch -p1 < ../wine-mf-encoder-support.patch
./configure --enable-win64 && make -j$(nproc)
```

## Requirements

GStreamer with H.264 encoding support (these should be installed already):
```bash
# Arch Linux
pacman -S gst-plugins-bad gst-plugins-good

# Ubuntu/Debian  
apt install gstreamer1.0-plugins-bad gstreamer1.0-plugins-good
```

## Usage

In Clip Studio Paint:
1. File → Export Animation → Movie
2. Choose MP4/H.264 format
3. Export

## Notes

- Non-standard resolutions (e.g., 902x1280) may have minor visual artifacts
- Standard resolutions (1920x1080, 1280x720) work perfectly
- Only tested with H.264 encoding

## License

LGPL 2.1 (same as Wine)
