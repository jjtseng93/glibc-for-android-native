- This is a fork of the GNU C Library with patches applied to comply with the Android App sandbox
- For more details on the patches, look at ./SOURCE_INFO
# News & Updates
- 2026/02/07: patched /etc/resolv.conf to /tmp/resolv.conf for libc.so.6 for Android use (requires adb shell or Shizuku on newer devices)
# Usage
## 1. Placing ld.so
- In the Android App sandbox, native binaries are not allowed to be executed directly unless placed within /data/app
- an example here: 
- /data/app/~~OfBa0tu6kShD611YZnDyaA==/com.drjohn.anci0-CrNSI-fAUPNofhmhLnO2Ug==/lib/arm64/libld-custom.so
- So you should first put ld.so into that folder when building your apk. 
- The corresponding path in apk is:
- lib/arm64-v8a/libld-custom.so
## 2. Calling ld.so
- lets assume you have ld.so put and aliased as ldcustom
- this is how you run a glibc binary
  + ldcustom --library-path /path/to/this/repo:/path/to/usr/lib/aarch64-linux-gnu ./path/to/binary
- or alternatively use
  + export LD_LIBRARY_PATH=/path/to/this/repo:/path/to/usr/lib/aarch64-linux-gnu
  + ./path/to/binary
- these 2 methods fits into different scenarios
  + if you will call external Android /system/bin binaries, use --library-path so that bionic libc programs still works
- be careful, if the binary is in the current folder, './binary' needs to be used instead of 'binary' directly
# Demo
- a working example App is in the pinned comment [here](https://www.threads.com/@johntz93/post/DULw-6qk4ib?xmt=AQF0AAh_hi9kuszx3aG-aAx1L0Xq07-Od72SquFG7qRgUg)
- In the Start GoTTY terminal, this repo is placed at ~/glibc, 
- you can get files into the App by curl or
  + $PKG_MDIR = /sdcard/Android/media/com.drjohn.anci0
