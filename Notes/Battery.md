# Battery note

My DSDT containes no "Embedded Control" so just install ACPIBatteryManager.kext and the battery work fine without patching DSDT.

However, sometimes the __battery icon__ (yes I mean the __icon__, not the _percentage_) display incorrectly. For example, follow these instruction to see that:

- Turn on your laptop and login to see the battery icon appear on the top right corner.
- Plugin your power adapter, the icon now in the "charging" state (a battery with lightning symbol in the middle).
- Then, put your laptop to sleep.
- When your laptop is sleeping, disconnect your power adapter.
- Wake it up again.

Now, we expect the battery icon is in the "normal" state (a battery with no lightning symbol), but it is still in the "charging" state.

The percentage always exactly although the battery icon display incorrectly. Maybe it's a bug in ACPIBatteryManager.kext.
