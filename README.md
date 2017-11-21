# arch-obs-studio-latest-ffmpeg-vaapi
obs studio latest version (non-git), with vaapi patch for hardware encoding on mesa, and obs-linuxbrowser

So I made a patch out of the ffmpeg-vaapi branch found here: https://github.com/w23/obs-studio/tree/ffmpeg-vaapi so it could easily be used on arch with obs-studio-git on the AUR rather than cloning + merging the repo every time there's an update. I've also edited the PKGBUILD so it pulls the latest release instead of the latest git commit version. 

requirements:
An intel or amd gpu that supports h.264 encoding, running on open source drivers (mesa). You may also need to install these packages:

libva-vdpau-driver  
libvdpau-va-gl  

for intel you may also need:  
libva-intel-driver  

install instructions on arch:  
sudo pacman -S libva-vdpau-driver libvdpau-va-gl  libva-intel-driver

git clone https://github.com/GloriousEggroll/arch-obs-studio-latest-ffmpeg-vaapi  
cd arch-obs-studio-latest-ffmpeg-vaapi  
makepkg -i  

Additional vaapi/vdpau driver instructions for Arch can be found here:  
https://wiki.archlinux.org/index.php/Hardware_video_acceleration#Installation  

Important notes:  
1. B-Frames are not supported by AMD VCE, leave this at 0 when using AMD GPUs.  
2. B-Frames can only be used on the "high" profile.  
3. Quality and QP are ignored when a bitrate higher than 0 is set. This is the vaapi/vdpau default.  
4. This is -ONLY- for open-source mesa. For nvidia nvenc please use proprietary drivers and NVENC option in obs.  
