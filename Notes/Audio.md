# Note about audio patching

You have two option to get your audio working (just choose one method):

1. Patch AppleHDA.kext
2. Using Lilu.kext + AppleALC.kext

I prefer the first method, cause I like to do thing by myself whenever I can.  
Choose the most suitable method for you, then go ahead.

---

## 1. Note for Patch AppleHDA.kext

I uploaded two version of AppleHDA.kext (already patched), one is for High Sierra (10.13.6) and another is for Mojave (10.14 beta 10). Please read carefully before using them.

Always backup your vanilla AppleHDA.kext before doing anything as you can restore it later if something went wrong.

Because I do not know "__Are _Pin complex, node ID,..._ the same on all devices that have the codec ALC282?__", so I uploaded my codec dump along with the patched AppleHDA.kext. You must compare yours and mine to verify if they are the same before using my patched AppleHDA.kext.

If they are not the same, use _Lilu.kext + AppleALC.kext_ method instead or patch the AppleHDA.kext by yourself.

If you do not know how to get your codec dump or how to patch AppleHDA, Google it or read the References section in my README.md for the _AppleHDA patching guides_.

---

### 1.1. Note for High Sierra (10.13.6)

1. Backup your vanilla AppleHDA.kext in /System/Library/Extensions (S/L/E in short)
2. Rename AppleHDA.10.13.6.kext to AppleHDA.kext
3. Install the patched AppleHDA.kext (in step 2) to S/L/E
4. Rebuild kext cache
5. Set CLOVER/config.plist/Devices/Audio/Inject = 28
6. Reboot

The following command can be used for the steps above:

```
# 1. Backup vanilla AppleHDA.kext
sudo mv /S*/L*/E*/AppleHDA.kext /Your_backup_folder_path/AppleHDA.kext

# Note:
# - Enter your password if required.
# - Replace "Your_backup_folder_path" with the actually backup path on your system.


# 2 + 3. Rename + Install patched AppleHDA.kext
sudo cp -R /Path_to_AppleHDA.10.13.6.kext /S*/L*/E*/AppleHDA.kext

# Note: Replace "Path_to_AppleHDA.10.13.6.kext" with the actually path on your system.


# 4. Rebuild kext cache
sudo kextcache -i /


# 5. Inject layout-id = 28
# No command for that step
# Use the plist editor (PlistEdit Pro, XCode) to edit this setting.
# Do not use other programs to edit plist file.

# 6. Reboot
sudo reboot
```

If you do not want to use terminal and command, just do it by hand and using your favorite tools (Kext Utility or something else). It's your choice.

---

### 1.2. Note for Mojave (10.14 beta 10)

1. Backup your vanilla AppleHDA.kext in /System/Library/Extensions (S/L/E in short)
2. Rename AppleHDA.10.14.kext to AppleHDA.kext
3. Install the patched AppleHDA.kext (in step 2) to S/L/E
4. Rebuild kext cache
5. Set CLOVER/config.plist/Devices/Audio/Inject = 4
6. Reboot

The commands are the same as for High Sierra (see section 1.1 above), except:

```
# 2 + 3. Rename + Install patched AppleHDA.kext
sudo cp -R /Path_to_AppleHDA.10.14.kext /S*/L*/E*/AppleHDA.kext

# Note: Replace "Path_to_AppleHDA.10.14.kext" with the actually path on your system.
```

---

## 2. Note for Using Lilu.kext + AppleALC.kext

Just get the lastest version of Lilu.kext and AppleALC.kext (see the References section in README.md for links to download kext).

Install these two kexts to /Library/Extensions (/L/E in short).

Set the CLOVER/config.plist/Devices/Audio/Inject value to the value that AppleALC.kext supported (you can find them in the Wiki page of AppleALC.kext).

Rebuild kext cache (see section 1.1 above for the command). Then reboot and you're good to go.