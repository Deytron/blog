---
title: "Getting the Meta Quest 2 to run on Linux"
date: "2024-02-13"
tags:
  - guide
  - linux
  - vr
thumbnail: "/assets/img/thumbnail/linux-vr.webp"
---

With the release of the Meta Quest 3, I just bought a second-hand Meta Quest 2 for 200€. Pretty cool device if you ask me. My question though was this : will my PCVR games work with Linux ? And the answer is: yes! But setup was painful. But working in the end.
Since there are not a lot of guide out there, and I still haven't started my own blog for this kind of thing, I'm writing a guide here and will save it for future use. The guide should still be relevant for months to come.

The guide seems pretty long, but it's actually pretty straightforward **if** you have almost the same setup as me. It may take around an hour to get everything running.

**TL;DR** :

- Setup was KDE Plasma 6 Wayland, Arch latest, AMD RX 6700 XT, Meta Quest 2 up-to-date
  - Should work 100% with Plasma 5
  - Nvidia GPU untested, you will have issues
  - Meta Quest 3 untested
- ALVR nightly 2024-02-11
- Half-Life Alyx, Borderlands 2 VR (yarr version)
  - Obviously paid version will work 100%
- Cheap TP-Link Wifi repeater (100Mbps)

On this rig, Half-Life Alyx works wirelessly perfectly. No latency.
Your mileage may vary depending on your setup, but if you got all this, you should be covered.

---

# Before purchasing anything

You should consider a few things before purchasing your VR headset, not exclusively related to Linux:

- Choose your headset depending on your budget, watch unbiased reviews on YouTube
  - Also check out the second-hand market
- A Windows dual-boot is more straightforward, if you want to play PCVR games right away
- You should have enough space in your room
- Meta WILL collect your data, keep that in mind when searching for your hardware
- Usual warnings about epilepsy, motion sickness and all, anyway make sure you're healthy enough

# Hardware/software check

- Nvidia tends to fare badly on Linux when it comes to VR, so you can try your luck but an AMD GPU is preferred
- Wayland/X11 should not matter, but you never know, switch to Wayland huh
- I'm currently on CachyOS (Arch), but an Ubuntu/Fedora distro is supported, though I won't be able to help much with that
- Make sure to set up your headset properly before starting

## Setup

This was the setup at the time of testing :

- Meta Quest 2 v62.0
- AMD RX 6700XT - Mesa-git v24.1.0-devel
- CachyOS base kernel, Linux v.6.7.4

[The installation guide is good](https://github.com/alvr-org/ALVR/wiki/Installation-guide), but I had to go further to get everything working. So in order:

### Developer mode

This step is needed to install ALVR on your headset. [Follow this guide to enable it](https://aixr.org/insights/how-to-enable-developer-mode-on-oculus-quest-2/).
As for the initial setup of the headset, this requires your Meta account and your smartphone but also your phone number.

### Sideloading ALVR client

- Install ADB: `paru -Sy android-tools`
- Download **alvr_client_android.apk** [here](https://github.com/alvr-org/ALVR-nightly/releases)

> **Make sure** the nightly APK package you download is the exact same as the PC version

- Turn on your Quest and plug it in your PC
- Wait for it to be detected, you will get in your headset's notification area a USB connection approval waiting. Tap it to enable USB Debugging.
  ![usb debugging](https://img.itch.zone/aW1nLzE0Njc1NjY2LmpwZw==/original/dLFJVP.jpg)
- Check that your device is listed by using `adb devices`. If it is _unauthorized_, make sure you tapped the notification
- `cd` to the same directory as the .apk file you downloaded, then use `adb install -g -r  alvr_client_android.apk`. You should see Success in your terminal after a few seconds.

ALVR should now be installed on your headset. You can find it in your Library, in the "Unknown Sources" category (top right).

**Pro tip:** Sideload [Lightning Launcher](https://github.com/threethan/LightningLauncher/releases/tag/7.1.1) if you want to see all your apps, including ALVR

### SteamVR and ALVR streamer

- _Optional_ Install Proton Experimental in your library
- Install [SteamVR](steam://launch/250820/Dialog) in your library. DO NOT use Proton on the software
  - Do NOT switch to Beta version
- Run it once, make sure it opens, then close it
- Download [ALVR-x86_64.AppImage](https://github.com/alvr-org/ALVR-nightly/releases) (only the AppImage worked for me for some reason)
  > **Make sure** the nightly AppImage you download is the exact same as the Quest version
- Run it, follow the setup wizard including downloading the PulseAudio script and the firewall rules
  - If you can't activate the firewall rules, add ports 9943 and 9944 to your firewall

## Connecting the headset

- Launch ALVR on your headset, and take note of the **client hostname** and the **IP Address**
- Launch ALVR on your PC, and click Launch SteamVR. Make sure SteamVR launches, and that ALVR displays Connected in green
- Click Add client manually, then enter the hostname and IP Address you got from the headset, then click save.
  - If you get the error "cannot find audio device which name contains "pipewire":
    - Type `paru -Sy pipewire-pulse`
    - Go to the Settings tab, scroll down until you see Audio and Microphone. Change both entries from _pipewire_ to _default_.

You should now see in your headset the SteamVR room.
From here, we will try launching Half-Life Alyx:

- Use the Pause/Start button on your left controller to display your Steam Library
- Find Half-Life Alyx, and make sure you have in the game's properties enabled Proton Experimental in the Compatibilty tab
  - Half-Life Alyx is one of the few games that might need the `-vr` argument added in properties
- Run the game, you should get rocks around you after a few seconds

# Known issues

- Half-Life Alyx crashes SteamVR when you quit. You will need to remove the headset and re-launch Steam
- Asynchronous Timewarp is not supported for now
- Bump up the bitrate if you notice that things are too blocky
