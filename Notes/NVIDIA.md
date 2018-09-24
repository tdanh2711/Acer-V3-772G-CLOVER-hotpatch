# Note for disable NVIDIA GTX 850M graphics card

Because Apple do not support NVIDIA card with Optimus technology, we need to disable it to save power.  
I use the following patches to disable my NVIDIA card:

- In CLOVER/config.plist/ACPI/DSDT/Patches:
  - Rename _SB.PCI0.LPCB.EC0._REG to _SB.PCI0.LPCB.EC0.XREG
  - Rename _SB.PCI0.PEG0.PEGP._INI to _SB.PCI0.PEG0.PEGP.XINI
  - Rename _SB.PCI0.PEG0.PEGP._OFF to _SB.PCI0.PEG0.PEGP.XOFF
- In CLOVER/ACPI/patched:
  - SSDT-DGPU.aml

You can go to **System Information > Graphics/Displays** to verify. If there is only the Intel HD Graphics 4600 graphics card, the patches above were worked.  
If not, you need to patch DSDT to disable your NVIDIA graphics card by yourself. Read post #3 in the **[Guide] Using Clover to "hotpatch" ACPI** to learn how to do that (you can found this guide in README.md > References section). My patches above is also a useful reference.