# arch-obs-studio-latest-ffmpeg-vaapi
obs studio latest version (non-git), with vaapi patch for hardware encoding on mesa

So I made a patch out of the ffmpeg-vaapi branch found here: https://github.com/w23/obs-studio/tree/ffmpeg-vaapi so it could easily be used on arch with obs-studio-git on the AUR rather than cloning + merging the repo every time there's an update. I've attached the patch and my pkgbuild. Also please note if you want to build OBS with the latest git commits rather than the latest stable release, change this line in the pkgbuild:

source=("$pkgname::git+https://github.com/jp9000/obs-studio.git#tag=20.1.3"

to include the tag of the release you want, like this:

source=("$pkgname::git+https://github.com/jp9000/obs-studio.git"

For other releases you can find release tags by going here: https://github.com/jp9000/obs-studio, then clicking the branch dropdown, and then clicking tags.

I tested this on mesa 17.2.5 on arch on an amd rx vega 64, working well!
