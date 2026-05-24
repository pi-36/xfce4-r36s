# xfce4-r36s
Flash the DarkOSRE Debian 13 (Trixie) ARM64 image to the SD card, run the .bat file inside the boot folder to select the correct display panel for your device, boot the system, disable EmulationStation, install minimal XFCE with LightDM and Xorg drivers, enable SSH, and reboot into a stable lightweight desktop environment.

Flash the SD card first:
Download the correct DarkOSRE Debian 13 (Trixie) ARM64 image for your RK3326 handheld.
Use balenaEtcher or Rufus
Flash the .img or .img.xz file to the microSD card.
After flashing:
Open the SD card boot partition in Windows.
Go to the boot folder.
Run the included .bat file to select the correct LCD/display panel for your handheld before first boot.
Insert the SD card into the device and boot:
First boot can take several minutes while Debian expands the filesystem.

Log into the system:

username: ark
password: ark

Update package lists:

sudo apt update

Disable EmulationStation permanently:

sudo systemctl disable emulationstation
sudo systemctl stop emulationstation
sudo systemctl mask emulationstation

Install minimal XFCE desktop:

sudo apt install \
xorg \
xinit \
lightdm \
lightdm-gtk-greeter \
xfce4 \
xfce4-session \
xfwm4 \
xfdesktop4 \
xfce4-panel \
thunar \
dbus-x11 \
--no-install-recommends -y

Install RK3566-compatible Xorg video drivers:

sudo apt install \
xserver-xorg-video-fbdev \
xserver-xorg-video-modesetting -y

Configure LightDM:

sudo dpkg-reconfigure lightdm

Select:

lightdm

Enable graphical boot:

sudo systemctl enable lightdm

Install and enable SSH:

sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh

Find the IP address:

hostname -I

Connect from Windows:

ssh ark@DEVICE_IP

Reboot:

sudo reboot
Final result:
Debian 13 Trixie ARM64
Correct display panel selected
EmulationStation disabled
Minimal XFCE desktop
Automatic GUI boot with LightDM
SSH enabled
Stable setup without startx hacks
