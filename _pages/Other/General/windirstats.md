---
title: "WinDirStat is (kinda) dead, here are better tools"
date: "2024-05-29"
tags:
  - linux
  - windows
thumbnail: "/assets/img/thumbnail/file-hierarchy.png"
---

There's a chance that, like Winrar, you or someone you know is still using a good software that is now replaced by something way better. Today we're going to talk about WinDirStat and the numerous alternative softwares you can use, and I will rank them based on my personal opinion.

# Why WinDirStat is obsolete

I'm lying a bit here. WinDirStat is not 100% _obsolete_, it will still work fine on your computer, but the latest update dates back from **September 2007**, which is more than 15 years now. We can confidently say that it's not supported anymore, and since then, other alternatives have seen the day of light.

The reason WinDirStat is slow and new software are 1000x faster is because by design, WinDirStat is crawling through all the folders and files on your disk to see what's present and their size. This is a rather time-consuming process, and uses a lot of your disk resource. Newer softwares now use the **MFT table** on your disk. The **M**aster **F**ile **T**able, as its name implies, is a sort of database for your NTFS disk that indexes all your files and "keeps" their location, for faster retrieval by your OS.

> ❔ But wait, on Linux disks are formatted in Ext4 and not NTFS, how come you can have softwares that work like this on other disk file fomats ?

Good question. Let me know if you have the answer to that. My guess is that Ext4 has something similar under the hood

# The best one

_Reminder that this is my personal opinion here_

## Cross-platform

### SquirrelDisk

<img src="https://www.squirreldisk.com/images/squirrel.png" style="width:200px;"/>

Okay so this one is pretty new. It's cross-platform, meaning you can use it on all of your OSes, Windows Mac and Linux alike. It's still a bit rough on the edge but it has almost everything you could need.

Pros:

- Pretty fast
- Really good UI, circle view and list view
- Sort by anything
- Supports disks and folder analysis
- 100% free
- Open-source
- Corss-platform

Cons:

- A bit buggy on Windows
- No portable version on Windows, only `.msi` package

## For Windows

### Wiztree

<img src="https://antibodysoftware-17031.kxcdn.com/images/wiztree200x.png" style="width:200px;"/>

A well known software, WizTree has been around for a long time now and as they say on their website, it's **46x faster than WinDirStat!**. Yeah, they're not exaggerating nor lying but that's just because as WinDirStat doesn't read the MFT table of your disk, it's gonna be very slow anyway.

Key points here:

- Very fast, few seconds to read multiple terabytes
- Pretty good UI, you have a list view and a block view
- Sort by anything
- Lots of options
- Supports disks and folder analysis
- Integrates into Windows Explorer context menu
- Has a portable version for quick usage

The only two cons here is that because of the way it works, it's Windows only, and simple nitpick but if you want to use it in an Enterprise environment, you will need to pay for an Enterprise License.

## For Linux

### For KDE: Filelight

<img src="https://apps.kde.org/app-icons/org.kde.filelight.svg" style="width:200px;"/>

From the KDE team, and thus deeply integrated into KDE, is FileLight. Basically the same thing as WizTree for Windows, but open-source. If you're on KDe, there is a high chance that you already have this installed. Otherwise you can use your favorite package manager to easily install it.

Key points here:

- Pretty fast
- Clean UI, respects your DE theme and you have a list view and a block view
- Can be opened from any folder
- Sort by anything
- Supports disks and folder analysis
- 100% free
- Open-source

### For Gnome: Baobab

<img src="https://gitlab.gnome.org/GNOME/baobab/-/avatar" style="width:200px;"/>

For those of you using Gnome, it's basically the same thing as Filelight but for the Gnome UI. Pros are exactly the same, and if you're using Ubuntu, it should already be installed.

## For Mac

### Baobab

Quite the esoteric choice here. Baobab is Gnome's disk file visualizer utility, and it _should_ be a Linux exclusive. So how come it works on MacOS? Well, I'll save you all the technical explanation, but basically MacOS and Linux are not that different from one another, and if a software checks some boxes, it can work on one OS or the other.

Key points here:

- Very fast
- Clean UI, integrates with MacOS and you have a list view and a block view
- Sort by anything
- Supports disks and folder analysis
- 100% free
- Open-source

Easiest way to install it would be to first install [Brew](https://brew.sh/) then use `brew install baobab`

## Honorable mentions

## For Windows

### FileLight

Yes, there is a Windows version of KDE team's FileLight that you can download [here](https://apps.kde.org/fr/filelight/).

Pros:

- Pretty fast
- Clean UI
- Sort by anything
- Supports disks and folder analysis
- 100% free
- Open-source

Cons:

- As it wasn't originally made for Windows, bugs can be present
- Downloadable on the Windows Store only
- Minimum version: Windows 10, Windows Server 2016

### TreeSize

<img src="https://images-eds-ssl.xboxlive.com/image?url=4rt9.lXDC4H_93laV1_eHHFT949fUipzkiFOBH3fAiZZUCdYojwUyX2aTonS1aIwMrx6NUIsHfUHSLzjGJFxxjGP4QeDYBE3DdDCqCfj640Qvfgxfi6yk2oVQk0wdePxUpTQ4bp4aBapo6j2ksY8AQ1dsneAAg_g.wIhNl_5lPM-&format=source" style="width:200px;"/>

TreeSize has been around for longer than WizTree, and has a few more features than it, but those features are not in the free version. A One-time buy will unlock you all the features.

Pros:

- Fast enough
- Functional UI, multiple views
- Sort by anything
- Supports disks and folder analysis
- Pro version allows to create PDF, HTML reports

Cons:

- Free version is pretty limited
- High price, even for one-time buy
- No portable version
- Pretty big

### SpaceSniffer

<img src="https://www.zwodnik.com/media/cache/93/cf/93cf3c6a555fa07dad9b7ed0e8ea5aec.png" style="width:100px;"/>

This one is preferred by old people, really. I keep it in the honorable mentions as it still functions to this day and it's free, but with the existence of Wiztree, there is absolutely no point in using this one.

Pros:

- Free

Cons:

- Very slow
- Absolutely terrible UI
- Not maintained
- Only one block view, no list view
- Not many settings

## For Mac

### Daisy Disk

<img src="https://static-00.iconduck.com/assets.00/apps-daisydisk-icon-2048x2048-e6tinsir.png" style="width:200px;"/>

This one is actually very cool. If you don't want to bother with your terminal, for the price of a McDonald's meal (sigh), you can get Daisy Disk.

Pros:

- Extremely fast
- The best UI, integrates well with MacOS
- List view and circle view
- Sort by anything
- Supports disks and folder analysis

Cons:

- MacOS only
- Price is 9.99€/$

## For Linux

### QDirStat

<img src="https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/qdirstat-logo.png" style="width:100px;"/>

This one is only if you don't want to install your DE's disk analyzer. QDirStat is based on KDirStat and removes all the previsous dependencies, as well as update it to Qt5. The UI is 99% the same as WizTree, so if you are too used to WizTree and don't want to change,

Key points:

- Very fast
- Clean UI, respects your DE theme and you have a list view and a block view
- Sort by anything
- Supports disks and folder analysis
- 100% free
- Open-source

**TL;DR** Use Wiztree on Windows, and FileLight or Baobab on anything else
