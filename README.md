Fennec DOS
==========

Overview
--------
Fennec DOS is basically Orfox (Tor Browser Android), but without routing over Tor network and upstream Firefox (instead of a modified ESR).
It enables many features upstreamed by the Tor Uplift project through @pyllyukko's user.js project.
It was originally created as builds of the patchset from [bug 1419581](https://bugzilla.mozilla.org/show_bug.cgi?id=1419581).

Faster builds
-------------
Use of ccache is extremely recomended as it will greatly speedup future builds.
Read [here](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/ccache)


Basic steps to build Fennec DOS (first build)
---------------------------------------------
- mkdir FennecDOS && cd FennecDOS
- git clone |THIS REPO| FennecDOS-Build
- git clone https://github.com/mozilla/gecko-dev.git
- cd gecko-dev
- git checkout esr60 #Choices: master (nightly), release (stable), esr60 (lts)
- ./mach bootstrap #Choose Android non-artifact
- cat ../FennecDOS-Build/Preferences/hardening.js >> mobile/android/app/mobile.js
- cp -r ../FennecDOS-Build/Branding/divestos mobile/android/branding/
- cp ../FennecDOS-Build/MOZCONFIG .mozconfig
- nano .mozconfig #Update paths
- ./mach build && ./mach package
An apk will be outputted into obj-arm-linux-androideabi/dist/

Basic steps to clean workspace and build (future builds)
--------------------------------------------------------
- git add -A && git reset --hard
- git pull
- cat ../FennecDOS-Build/Preferences/hardening.js >> mobile/android/app/mobile.js
- cp -r ../FennecDOS-Build/Branding/divestos mobile/android/branding/
- rm -rf obj-arm-linux-androideabi
- ./mach build && ./mach package
An apk will be outputted into obj-arm-linux-androideabi/dist/

NDK r17 arm failure fix
-----------------------
See https://bugzilla.mozilla.org/show_bug.cgi?id=1489384
- sed -i 's/r17b/r15c/' python/mozboot/mozboot/android.py;
- ./mach bootstrap

TODO
----
- Default Settings
- Default Search
- Default top sites
- Further pilfer patches from Tor Browser Android
