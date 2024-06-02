---
title: "How to bypass Steam's Family Sharing restrictions"
date: "2024-06-02"
tags:
  - linux
  - windows
  - steam
thumbnail: "/assets/img/thumbnail/familysharethumb.jpg"
---

Steam's Family Sharing is Valve's way to let your family members enjoy the games you own when you're not playing them. You can allow **up to five accounts** to use your library. The current restriction is that your other family members cannot play your games if you are playing _any_ of your games in your library. Future updates will make it so the other members will be able to play any game in your library as long as you're not playing the same one.

There is a way that is both Windows and Linux compatible to bypass theses restrictions. This is the topic of this post.

> Will this still work with the announce of the overhaul of the Family Sharing system?

Technically speaking, this method should still work as core files should be unchanged. But there's still a slight chance that it could break, we never know. I will update this post accordingly when the feature drops on Steam stable branch.

# Setup Family Sharing

To setup Family Sharing, do the following steps:

1. Family Sharing works by account **and** by device, so first log in with the other family members account **on** the computer that is going to be used.
2. Once this is done, switch account and log in with the account that **owns the games** you want to share.
3. Once logged in, click in the top left _Steam_ tab > Settings > Family, then enable **Authorize Library Sharing on this computer**.
4. You will then see a list of the other accounts that are connected on the computer. Enable up to 5 accounts in the list, then close settings.
5. Once this is done, you can switch with any of the other logged in account and you should be able to **borrow** any newly available game.

# Bypass Family Sharing restrictions

Now that everything is setup, close Steam and follow the steps, they are different depending on your OS.

## 🪟 Windows

1. Head [here](https://cs.rin.ru/forum/viewtopic.php?f=29&t=103709&hilit=greenluma) and download the zip archive at the bottom of the post. You **will** need an account and a password to download the file, and unfortunately I can't help you with that here.
2. Once you downloaded the archive, to bypass Family Sharing restrictions, you will only need to use the _Stealh Mode_. Head to `C:\Program Files (x86)\Steam`, then open your downloaded zip file, and put the two files `user32.dll` and `DeleteSteamAppCache.exe` into your Steam install folder.
3. Open Steam and if on any of the shared games, you see **Play** instead of **Borrow**, you should be good to go!

## 🐧 Linux / Steam Deck

> If you're on Steam Deck, first head to desktop mode

1. Open your favorite terminal or Konsole.
2. Copy and paste the following commands:

```bash
sudo cp "/home/$USER/.steam/bin32/steamclient.so" "/home/$USER/.steam/bin32/steamclient\_backup.so" \

sudo cp "/home/$USER/.steam/bin32/steamclient.so" . \

sudo chmod 777 ./steamclient.so \

echo -e "0028ae60: 31c040c3\\n0028eef0: 31c040c3\\n009a6930: 31c040c3" | xxd -r - ./steamclient.so \

sudo chmod 555 ./steamclient.so \

sudo cp ./steamclient.so "/home/$USER/.steam/bin32/steamclient.so"
```
3. If no error is thrown, then you can simply open Steam and if on any of the shared games, you see **Play** instead of **Borrow**, you should be good to go!

# Know issues

- For obvious reasons, free-to-play games and those that have Family Sharing explicitly disabled are not supported
- With the bypass active, updates won't download and install properly. To fix this, simply move the file `user32.dll` somewhere else temporarily, then run `DeleteSteamAppCache.exe`, open Steam and download your updates, then close Steam, move the file back in the install folder, and you should be good.
- You may be interested in a few other features that GreenLuma offers on Windows, but they're unavailable on Linux. For now at least

# Can I get banned for this?

This obviously goes against Steam's TOS, but there hasn't been any report of anyone getting ban from Steam by using this bypass to play. Also, think about it this way: you're still buying from Steam anyway and using their services, so there isn't much point to block you.

# Credits

All the credits go to `CowedCow` on RIN for the Rust setup and `u/yobbbu` for the Reddit post, as well as `Mattys0082` for the easier setup