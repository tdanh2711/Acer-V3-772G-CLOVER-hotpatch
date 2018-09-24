# Note for Fn keys

In my laptop, all Fn keys work fine after install VoodooPS2Controller.kext, except the brightness key (Fn + Left/Right arrow) and toggle Wi-Fi key (Fn + F3).

These two function keys not generate a PS2 key code, it make an EC query instead, so we need to find the EC query method in DSDT and patch it.

For more information, read the __[Guide] Patching DSDT/SSDT for LAPTOP backlight control__ in the README.md > References section.

---

## 1. Implement the brightness key (Fn + F3)

First, try to use my brightness key patch:

- CLOVER/config.plist/ACPI/DSDT/Patches/...Brightness key down
- CLOVER/config.plist/ACPI/DSDT/Patches/...Brightness key up
- CLOVER/ACPI/patched/SSDT-BrightnessKey.aml

Reboot. Then use the Fn + brightness key on your laptop to verify if my patch work fine on your system.

If it not, that mean your DSDT is difference to me. Try to patch the brightness key yourself (read the guide I mentioned above).

On my laptop, the Fn + Left arrow (brightness down) call the EC query method name _Q71, and the Fn + Right arrow (brightness up) call the EC query method name _Q70. You need to find the right EC query methods that your brightness key call in your system and patch it. Use the guide above and my SSDT-BrightnessKey.aml as a reference.

---

## 2. Implement the Toggle Wi-Fi key

Because macOS has no built-in toggle Wi-Fi function key, we need to create a service to do that.

1. Open Automator app (you can find it in Launchpad).
2. Choose Service (on High Sierra) or Quick Action (on Mojave).
3. Choose _Utilities_ on the left column.
4. Drag and drop the _Run Shell Script_ on the 2nd column to the workspace.
5. Copy and paste the following code to you new Service/Quick Action (please read and do the __Note__ below carefully).

```
// Create a service to toggle Wi-Fi
// Note: Change en1 to the actual wifi network interface (run ifconfig to determine)

if [[ `networksetup -getairportpower en1` == *On ]]
then
  networksetup -setairportpower en1 off
else
  networksetup -setairportpower en1 on
fi
```

6. Change _Workflow receives current_ to _No input_.
7. Save the Service/Quick Action (Command + S), name it "__Toggle Wi-Fi__" (or whatever you want).
8. Go to __System Preferences > Keyboard > Shortcuts > Services__.
9. Scroll down to bottom, you will see your new Service here. Give it a shortcut.

_**Note**: Recommend using the **Command + F3** or a shortcut that have the Command key. For example: Command + Ctrl + F, Command + Option + G,... any shortcut you want but must have the Command key in it. Otherwise the shortcut will not work as expected (this is a known bug ever in a real mac, you can Google it)._

The last step is using my Toggle Wi-Fi patch:

- CLOVER/config.plist/ACPI/DSDT/Patches/...Toggle WiFi
- SSDT-ToggleWiFiKey.aml

_**Note**: If you used the **Command + F3** key as I suggested, nothing to do here. But if you used another shortcut, you must change the **SSDT-ToggleWiFiKey.aml** to match your new shortcut. Refers to the guide I mentioned in section 1 above as a reference._

Reboot. Then use the Toggle WiFi key on your laptop (mine is Fn + F3) to verify if the patch is working.

If everything OK, congratulation! You're done!

If not, you have to patch the Toogle Wifi key yourself. Read the guide I mentioned in the section 1 above for the idea of **find + patch EC query method and key mapping**. My **SSDT-ToggleWiFiKey.aml** is also a useful reference.
