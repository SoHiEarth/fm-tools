# Forza Motorsport on Linux using `GE-Proton11-3-FM` and `xodus`

> [!IMPORTANT]
> **Please make a backup of this repo or fork it so it doesn't become lost history (again)**

## Dependencies
- `kwallet`, with the desktop environment preferably KDE Plasma. The wallet should be open while xodus is running.
- `webkit2gtk-4.1` [Reference](https://archlinux.org/packages/extra/x86_64/webkit2gtk-4.1/)

## Instructions
1. Unzip `GE-Proton11-3-FM.zip`

2. Copy `/GE-Proton11-3-FM` to `~/.steam/steam/compatibilitytools.d`

3. Make Steam use GE-Proton11-3-FM for Forza Motorsport (Steam -> Library -> Forza Motorsport -> Properties -> Compatibility)

  > [!TIP]
  > If you don't see GE-Proton11-3-FM, restart Steam.

4. Log into xodus (`/path/to/xodus-cli login`)

  > [!TIP]
  > Getting weird login errors at this stage? Make sure you have `kwallet` available.
  > 
  > For Wayland/NVIDIA users: Using this command may resolve window issues:
  > 
  >   `WEBKIT_DISABLE_DMABUF_RENDERER=1 /path/to/xodus-cli login`

5. Start xodus-service (`./path/to/xodus-service`)

  > [!IMPORTANT]
  > Keep this running before the game starts. It is required for the game to communicate with online servers.

  > [!TIP]
  > Autostart it with your system or make it start on demand ([reference](https://blog.volc.men/blog/forza-motorsport-linux/#running-xodus-only-while-forza-runs))

6. Retrieve a copy of `xgameruntime.dll` and rename it to `xgameruntime.dll.threading`

  > [!TIP]
  > A Windows installation with "Gaming Services" installed will have this file in the `system32` directory.

  > [!WARNING]
  > Downloading a copy from dll downloaders may not work!

7. Copy `xgameruntime.dll.threading` to where `forza_steamworks_release_final.exe` is stored at.
8. Copy `xgameruntime.dll.threading` to `~/.steam/steam/steamapps/compatdata/2440510/pfx/drive_c/windows/system32/`
9. Set the launch options of Forza Motorsport to `PRESSURE_VESSEL_FILESYSTEMS_RW=/run/user/1000/xodus.sock WINEDLLOVERRIDES=xgameruntime=b PROTON_VKD3D_HEAP=1 VKD3D_CONFIG=skip_application_workarounds,descriptor_heap,avoid_image_buffer_aliasing %command%`

  > [!TIP]
  > Users have reported controllers to work w/o Steam Input by adding `PROTON_DISABLE_HIDRAW=1` to the beginning of their launch options.

9. Profit!

  > [!TIP]
  > If Forza crashes at the title screen, checking if the "Default Keyring" wallet was opened and opening it fixed the issue.
  > I also tried the `linux-hardened` kernel, but it didn't work on my end.

## Compatibility

xodus-cli and xodus-service built using Arch Linux.

I don't have an AMD system, so I can't verify if these instructions work on AMD GPUs.

Verified using the following configuration:

- GPU: NVIDIA GeForce RTX 3060 (Driver: nvidia-open-dkms 615.71.09-1)
- Kernel: Linux 7.2.8-zen1-2-zen
- Desktop Environment: KDE Plasma 6.7.5
