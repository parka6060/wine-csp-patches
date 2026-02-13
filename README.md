# Wine Patches for Clip Studio Paint Video Export

Adds H.264 video encoding support to Wine so Clip Studio Paint can export animations and timelapses. These patches are only tested with CSP running under wine, and is not intended to be a proper implimentation of the WindowsMF api. **Provided as-is with no support** - this is a working solution for a specific program.

## Install

**Pre-built DLLs** (in `release/` folder):
RECOMMENDED: For Bottles - copy the dll files into your bottles system 32.
- In the bottles interface hit 'Browse', go to drive_c/windows/system32/
- Copy the two DLL files from release>windows.

# System Wine (requires root)
sudo cp release/x86_64-windows/*.dll /usr/lib/wine/x86_64-windows/
sudo cp release/x86_64-unix/*.so /usr/lib/wine/x86_64-unix/
```

**Or apply patch to Wine source:**
```bash
cd wine-source # where your wine source is
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
- Changing the video export animation framerate from the default will break encoding, I'll see if i have time for a fix. However default (24fps) exports for animations work.
- Timelapses work flawlessly.

## License

LGPL 2.1 (same as Wine)
