# arch-obs-studio-latest-ffmpeg-vaapi
obs studio latest version (non-git), with vaapi patch for hardware encoding on mesa

So I made a patch out of the ffmpeg-vaapi branch found here: https://github.com/w23/obs-studio/tree/ffmpeg-vaapi so it could easily be used on arch with obs-studio-git on the AUR rather than cloning + merging the repo every time there's an update. I've also edited the PKGBUILD so it pulls the latest release instead of the latest git commit version.
