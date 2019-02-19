## How to build a pgs4a distribution

Follow these instructions:

1. Get a virtual machine running Linux
    - for example, Xubuntu 64 bit, running with VirtualBox
  
2. Clone this repository
2. Download android NDK r13b, and put it in the cloned repository
    - this version still uses old headers so it will work with our toolchain, newer versions require edits
    - it can build apps with minimum android-9 platform API
3. Download android SDK
    - this may not be necessary at this time, but in case the toolchain needs it, api-9 could be installed in it, using ./sdkmanager "platforms;android-9"
    - sdk tools version 25.2.5 or older is even nicer; this will be used later when building apps, because android commands are still supported, and it has a nice GUI to install packages
4. Use pip install cython==0.20 to install older cython version, to avoid errors with jnius
4. Run ./build_pgs4a_new.sh. A pgs4a dist should be created in /dist
5. When something fails, most likely some paths have to be edited, for example in build_pgs4a_new.sh, /python-for-android/distribute_new.sh so all path match with the downloaded NDK

Now it's time to use the pgs4a dist!

## Used repositories

The following repositories where clones and edited:

* https://github.com/renpy/rapt

* https://github.com/kivy/python-for-android

1. Both clones used releases or commits from 12th june 2013
2. The recipe for pyjnius was edited, so the correct package was downloaded (also from that old date).
3. Edited the paths and files in both build_pgs4a and distribute shell scripts, and saved them as _new.sh
4. Edited sdl_androidinput.c: return 0 (add zero) to avoid compile error
5. Edit liblink: remove -arch option
6. Added rm -rf of build folders at the beginning of build_pgs4a.sh, so everything starts fresh on retry after something has failed.

