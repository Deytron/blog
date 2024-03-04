---
title: "Fixing Windows error ID 359 and related events"
tags:
  - windows-server
  - windows-hello
date: "2024-03-04"
thumbnail: "/assets/img/thumbnail/windows-error-359.png"
---

I've recently had to take care of a ticket where the client was complaining about errors filling his event viewer.

The main error was the following:

![error359](https://i.imgur.com/t1uto4C.png)

```
Windows Hello for Business provisioning has ecnountered an error during policy evaluation.
ExitCode: RPC Server is unavailable
Method: LsaGetSSOAccountType
See https://go.microsoft.com/fwlink/?linkid=832647 for more details
```

There were a few other errors coming up with the same Event ID, but with a different ExitCode:
`ExitCode: The system cannot find the file specified.
Method: WinStationIsSessionRemoteable`

All of these come from the same issue: For some reason, on this Windows Server, Windows Hello is enabled and, in my case, it was unused and not needed.

# The fixes

I actually applied two fixes that I found online to fix the issue. I don't exactly know which one stopped the errors from popping in the event viewer, but hey, at least it worked.

**Do not apply these fixes if your server uses Azure AD.** While this could fix the issue, it could also lead to undesirable side effects. I haven't tested enough, so do this at your own risk.

## 1. Disabling Windows Hello via GPO

This one is pretty simple.

- Press `⊞ Win` + `R` to open up the Run dialog, then `gpedit.msc`. This will open up the computer management window.

- From there, head to `Computer Config > Policies > Admin Templates > Windows Components > Windows Hello for Business` and set the toggle to _Enabled_ BUT also tick the **Do not start Windows Hello provisioning after login** box

![whello](https://i.imgur.com/lXt9ktc.png)

## 2. Disabling Windows Hello logs

This won't fix the issue, but it will fix the continuous logs in your event viewer.

- Open your registry editor with `regedit`

- Head to `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\Autologger\EventLog-Application\{23b8d46b-67dd-40a3-b636-d43e50552c6d}
` (you can copy-paste this in the title bar at the top)

- You should the an `Enabled` DWORD. Double-click and set the value to 0

- Reboot the server

This should disable all WIndows Hello logs in the event viewer.

## Final words

Remember, as an IT guy, you should **always fix the root cause of your issues**. Hiding logs or trying to ignore them will only lead to further issues later, so the second fix is far from ideal, but fortunately it seems that there is no real issue anyway. Windows has a tendency to spit out logs all the time without much reason.
