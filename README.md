# Ubuntu-Aero-15W
Updates to Ubuntu for Gigabyte Aero 15W-V8

## Graphics: Install the latest Nvidia drivers

## Graphics: Enable synchronization for Nvidia

Edit **/etc/systemd/system/display-manager.service**

Find: `ExecStartPre=/usr/share/gdm/generate-config`

Replace it with: `ExecStartPre=/usr/bin/xinit /usr/share/gdm/generate-config`

Create **/lib/modprobe.d/nvidia-kms.conf**

Add the following line to the file:
`options nvidia-drm modeset=1`

## Graphics: Fix switch from Intel to Nvidia

Enables external monitor without needing to restart.

Edit **/etc/gdm3/PostSession/Default**

Add the following before `exit 0`:

```
killall Xorg
systemctl restart gdm.service
```

## Graphics: Fix login screen - external display

Disable Wayland for the login screen.

Edit **/etc/gdm3/custom.conf**

**Before:** # WaylandEnable=false

**After:** WaylandEnable=false

## Audio: Add headset support

Edit **/etc/modprobe.d/alsa-base.conf**
Add the following line to the end of the file:
`options snd-hda-intel model=dell-headset-multi`
