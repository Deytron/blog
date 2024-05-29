---
title: "Playing your PCVR games on Linux without SteamVR"
date: "2024-05-28"
tags:
  - guide
  - linux
  - vr
thumbnail: "/assets/img/thumbnail/wivrn.svg"
---

If you're running Linux, you pretty much already know that VR is pretty hard to get running if the games you want to play are PCVR games.
Apart from ALVR, you don't have much of a choice, as SteamVR is broken and we're still waiting for Valve to work on it.

Fortunately we can thank the WiVRn team for their effort, as their solution allows us to not use SteamVR at all! WiVRn uses OpenComposite and Monado to get your games running wirelessly.

---

# Pre-requisites

WiVRn currently supports all Android-based headsets, as the installation package is a `.apk`. The most popular ones are the Meta Quest, the Pico headsets and the HTC Vive series.


## Installation if you want the latest features

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
