# Acer V3-772G CLOVER hotpatch

Last update 2018.09.21.0103 (GMT+7)

All kexts is placed in CLOVER/kexts/Other/Backup

Please read the README and all related notes carefully before using this CLOVER (list of Notes can be found near the bottom).

---

## CLOVER info

```
+----------------+--------------------------------+
| Clover version | v2.4k r4658                    |
+----------------+--------------------------------+
| Target macOSX  | High Sierra (10.13.6)          |
|                | Mojave Beta 10 (10.14 Beta 10) |
+----------------+--------------------------------+
| Patch method   | 100% hotpatch                  |
+----------------+--------------------------------+
```

---

## System info

```
+-------------+-----------------------------------------------+
| CPU         | Intel Core i7-4712MQ                          |
+-------------+-----------------------------------------------+
| VGA         | Intel HD Graphics 4600                        |
|             | NVIDIA GTX 850M (Optimus)                     |
+-------------+-----------------------------------------------+
| Ethernet    | Broadcom Limited NetLink BCM57780 [14e4:1692] |
+-------------+-----------------------------------------------+
| Wireless    | Qualcomm Atheros AR9462 [168c:0034]           |
+-------------+-----------------------------------------------+
| Audio codec | ALC282                                        |
+-------------+-----------------------------------------------+
| USB         | EHCI (2 port)                                 |
|             | XHCI (2 port)                                 |
+-------------+-----------------------------------------------+
| Card reader | Realtek RTS5209 [10ec:5209]                   |
+-------------+-----------------------------------------------+
```

---

## Working

```
+----------------+-------------------------------------------------------------------------+
| CPU            | Speedstep (Power management) enabled                                    |
+----------------+-------------------------------------------------------------------------+
| VGA            | Intel HD Graphics 4600 full QE/CI                                       |
+----------------+-------------------------------------------------------------------------+
| Ethernet       | OK                                                                      |
+----------------+-------------------------------------------------------------------------+
| Audio codec    | Patch AppleHDA by myself (please read note #1)                          |
|                | You can use AppleALC.kext instead                                       |
+----------------+-------------------------------------------------------------------------+
| USB            | OK. Work well after wake up from sleep                                  |
+----------------+-------------------------------------------------------------------------+
| Battery        | Percentage always display exactly                                       |
|                | Sometimes battery icon display incorrectly (please read note #2)        |
+----------------+-------------------------------------------------------------------------+
| Fn key         | - Brightness (Fn + Left/Right)                                          |
|                | - Volume & mute (Fn + Up/Down, Fn + F8)                                 |
|                | - Toggle wifi (Fn + F3)                                                 |
|                | - Sleep (Fn + F4)                                                       |
|                | - Turn off display (Fn + F6)                                            |
|                | - Toggle trackpad (Fn + F7)                                             |
|                | - Play/pause, stop, previous, next (Fn + Home, Pg Up, Pg Down, End)     |
|                | Please read note #3 if you want to implement the Fn key correctly       |
+----------------+-------------------------------------------------------------------------+
| Other function | Sleep, Restart, Shutdown OK                                             |
|                | Wake up from sleep OK (Please read note #4)                             |
|                | iMessage & Facetime OK                                                  |
+----------------+-------------------------------------------------------------------------+
```

---

## Not working

```
+-------------+-----------------------------------------------------------+
| VGA         | NVIDIA GTX 850M disabled (Apple does not support Optimus) |
|             | Please read note #5                                       |
+-------------+-----------------------------------------------------------+
| Wireless    | Kext available but not working properly                   |
|             | Please read note #6                                       |
+-------------+-----------------------------------------------------------+
| Card reader | Kext not available                                        |
+-------------+-----------------------------------------------------------+
```

---

## Notes

- [Note #1: Audio](Notes/Audio.md)
- [Note #2: Battery](Notes/Battery.md)
- [Note #3: Fn keys](Notes/FnKeys.md)
- [Note #4: Wake up](Notes/WakeUp.md)
- [Note #5: Disable NVIDIA](Notes/NVIDIA.md)
- [Note #6: Atheros AR9462 Wireless card](Notes/AR9462.md)

---

## References

This is my first hackintosh (and also the first time I using hotpatch, of course). It's really a long journey with many knowledge and experiences. I just cannot finish without the help of some people and their useful tutorials, kexts and patchs. I would like to say a special thank you to all of these guys:

- tonymacx86 @tonymacx86.com for the macOS High Sierra installation guide. This is the place where everything was started.
- RehabMan @tonymacx86.com for all DSDT patching guides, kexts and helped me figure out the problem when I tried to implement the backlight control. All your works is really incredible!
- MaLd0n @insanelymac.com for helped me static patch my DSDT. I compared it with my original DSDT to make some important decisions during the process of implement hotpatch.
- 1and1get2 @tonymacx86.com for the graphics glitch patch for HD4600 on High Sierra 10.13.6 and Mojave 10.14 beta 10.  I tried all the solutions I've found on the internet with no success. Only yours worked!
- niemtin007 @niemtin007.blogspot.com, Tô Hùng Dương @duongth.com and some other guys with their blogs about patching DSDT, dictionary of current available kexts, basic knowledge of hackintosh and many useful tips & experiences.
- Trung Nguyên Nguyễn @trungnguyenblogs.blogspot.com, EMlyDinEsH @osxlatitude.com with their AppleHDA patching guides. My audio working perfectly now!
- adlan @osx86.com for the original BCM5722D.kext (Ethernet kext) and chris1111, long1eu for the BCM5722D.kext ver 2.3.7 (fix bug ethernet not working after wake up from sleep).
- And too many other people that I cannot remember now.

Thank you all very much!

Here are some important posts/tutorials/guides that I've been followed so far:

- [UniBeast: Install macOS High Sierra on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-high-sierra-on-any-supported-intel-based-pc.235474/)
- [[Guide] Patching LAPTOP DSDT/SSDTs](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/)
- [[Guide] Using Clover to "hotpatch" ACPI](https://www.tonymacx86.com/threads/guide-using-clover-to-hotpatch-acpi.200137/)
- [[Guide] Patching DSDT/SSDT for LAPTOP backlight control](https://www.tonymacx86.com/threads/guide-patching-dsdt-ssdt-for-laptop-backlight-control.152659/)
- [[Guide] Laptop backlight control using AppleBacklightInjector.kext](https://www.tonymacx86.com/threads/guide-laptop-backlight-control-using-applebacklightinjector-kext.218222/)
- [modified clover with edid patch to fix boot second stage garbled screen](https://www.tonymacx86.com/threads/modified-clover-with-edid-patch-to-fix-boot-second-stage-garbled-screen.238918/)
- [[Guide] Patch DSDT cho máy Hackintosh (Phần 5) ](https://niemtin007.blogspot.com/2015/05/guide-huong-dan-patch-dsdt-cho-may.html)
- [Phần 1: Cách Hackintosh của newbie hầu hết đều sai.](http://www.duongth.com/2017/07/phan-1-cach-hackintosh-cua-newbie-viet.html) (and all other posts in this series)
- [[Hướng dẫn] Patch AppleHDA cho các laptop chạy Hackintosh](http://trungnguyenblogs.blogspot.com/2015/10/huong-dan-patch-applehda-cho-cac-laptop.html)
- [Complete AppleHDA Patching Guide](https://osxlatitude.com/forums/topic/1946-complete-applehda-patching-guide/)
- [AppleHDA Binary Patching](https://osxlatitude.com/forums/topic/1967-applehda-binary-patching/)
- [Patch Apple HDA.](https://tinhte.vn/threads/patch-apple-hda.1481524/)

Here is the list of kexts I used:

- [GitHub - RehabMan/OS-X-FakeSMC-kozlek](https://github.com/RehabMan/OS-X-FakeSMC-kozlek)
- [GitHub - RehabMan/OS-X-Fake-PCI-ID](https://github.com/RehabMan/OS-X-Fake-PCI-ID)
- [GitHub - acidanthera/Lilu](https://github.com/acidanthera/Lilu)
- [GitHub - acidanthera/AppleALC](https://github.com/acidanthera/AppleALC)
- [GitHub - acidanthera/WhateverGreen](https://github.com/acidanthera/WhateverGreen)
- [GitHub - RehabMan/OS-X-ACPI-Battery-Driver](https://github.com/RehabMan/OS-X-ACPI-Battery-Driver)
- [GitHub - adlan/BCM5722D](https://github.com/adlan/BCM5722D)
- [GitHub - chris1111/BCM5722D](https://github.com/chris1111/BCM5722D)
- [GitHub - RehabMan/OS-X-Voodoo-PS2-Controller](https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller)
- [GitHub - RehabMan/OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All)
- [Insanelymac - AirPortAtheros40.kext v21](https://www.insanelymac.com/forum/topic/312045-atheros-wireless-driver-os-x-101112-for-unsupported-cards/?do=findComment&comment=2509900)
- [GitHub - black-dragon74/ATH9KFixup](https://github.com/black-dragon74/ATH9KFixup)

---