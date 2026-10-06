# Forza Motorsport on Linux using `GE-Proton11-3-FM` and `xodus`

> [!IMPORTANT]
> Please make a backup of this repo or archive it so it doesn't become lost history (again)

## Instructions
1. Unzip `GE-Proton11-3-FM.zip`
2. Setup GE-Proton11-3-FM
Copy `/GE-Proton11-3-FM` to `~/.steam/steam/compatibilitytools.d`

3. Make Steam use GE-Proton11-3-FM for Forza Motorsport
Steam -> Library -> Forza Motorsport -> Properties -> Compatibility

> [!TIP]
> If you don't see GE-Proton11-3-FM, restart Steam.

4. Log into xodus
For Wayland/NVIDIA: `WEBKIT_DISABLE_DMABUF_RENDERER=1 /path/to/xodus-cli login`

> [!TIP]
> Getting weird login errors at this stage? Make sure you have kwallet available.

5. Start xodus-service (and keep it running!)
`./path/to/xodus-service`

> [!TIP]
> Autostart it with your system or make it start on demand ([reference](https://blog.volc.men/blog/forza-motorsport-linux/#running-xodus-only-while-forza-runs))

6. Retrieve a copy of `xgameruntime.dll` and rename it to `xgameruntime.dll.threading`
Get a genuine copy of `xgameruntime.dll` from the system32 folder of a Windows installation with "Gaming Services" installed.

> [!WARNING]
> Downloading a copy from dll downloaders do not work!

7. Copy `xgameruntime.dll.threading` to where `forza_steamworks_release_final.exe` is stored at.
8. Copy `xgameruntime.dll.threading` to `~/.steam/steam/steamapps/compatdata/2440510/pfx/drive_c/windows/system32/`
9. Set the launch options of Forza Motorsport to `PRESSURE_VESSEL_FILESYSTEMS_RW=/run/user/1000/xodus.sock WINEDLLOVERRIDES=xgameruntime=b PROTON_VKD3D_HEAP=1 VKD3D_CONFIG=skip_application_workarounds,descriptor_heap,avoid_image_buffer_aliasing %command%`

> [!TIP]
> Users have reported controllers to work w/o Steam Input by adding `PROTON_DISABLE_HIDRAW=1` to the beginning of their launch options.

9. Profit!

## Compatibility
xodus-cli and xodus-service built using Arch Linux.
I don't have an AMD system, so I can't verify if these instructions work on AMD GPUs.
Verified using the following configuration:
GPU: NVIDIA GeForce RTX 3060 (Driver: nvidia-open-dkms 615.71.09-1)
Kernel: Linux 7.2.8-zen1-2-zen
Desktop Environment: KDE Plasma 6.7.5
