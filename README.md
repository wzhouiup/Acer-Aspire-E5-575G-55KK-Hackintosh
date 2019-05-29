# Acer-Aspire-E5-575G-55KK-Hackintosh
Hackintosh guide for the Acer E15 series E5-575G-55KK laptop

**Main Specs:** 
* Intel i5-7200u
* IGPU: Intel HD 620
  * DGPU: Nvidia 940mx 2GB (disabled)
* Realtek ALC255
* I2C touchpad when "Advanced" touchpad selected in BIOS

## Instructions:

**Important!**
Use the original Clover bootloader from https://sourceforge.net/projects/cloverefiboot/ when following [this laptop guide for UEFI.](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)

-----
**Follow the guide in order to create the bootable USB. For reference, the kexts I started off for the installation are as follows:**

   > FakeSMC  
   > WhateverGreen  
   > Lilu  
   > RealtekRTL8111  
   > VoodooPS2Controller

Use config_HD615_620_630_640_650.plist from the guide. I recommend using [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) if/when making changes to a .plist.

-----

**Follow these guides after installation**
   
[Patching DSDT/SSDTs](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/)

[Disabling the Nvidia 940MX](https://www.tonymacx86.com/threads/guide-disabling-discrete-graphics-in-dual-gpu-laptops.163772/)

[Brightness control](https://www.tonymacx86.com/threads/guide-laptop-backlight-control-using-applebacklightfixup-kext.218222/)

[Touchpad I2C](https://voodooi2c.github.io/)

-----

**Fixing audio**

   **Note:** *Use Layout 3 for any audio related patching, and simply inject in .plist (in Clover Configurator) when ready*
   
   [Audio w/ AppleALC kext](https://www.tonymacx86.com/threads/an-idiots-guide-to-lilu-and-its-plug-ins.260063/#AppleALC)
   
   To fix the garbled/warped audio through headphones, install CodecCommander kext and create a new file in MaciASL named SSDT-ALC255.aml in /EFI/Clover/ACPI/patched containing:
   
   ```
   // Credit to insanelydeepak
   // CodecCommander configuration for ALC255 to fix various issue 
// repo: https://github.com/insanelydeepak/cloverHDA-for-Mac-OS-Sierra-10.12

DefinitionBlock ("", "SSDT", 1, "hack", "_ALC255", 0)
{
    External(_SB.PCI0.HDEF, DeviceObj)
    Name(_SB.PCI0.HDEF.RMCF, Package()
    {
        "CodecCommander", Package()
        {
            "Custom Commands", Package()
            {
                Package(){}, // signifies Array instead of Dictionary
                Package()
                {
                    // 0x19 SET_PIN_WIDGET_CONTROL 0x24
                    "Command", Buffer() { 0x01, 0x97, 0x07, 0x24 },
                    "On Init", ">y",
                    "On Sleep", ">n",
                    "On Wake", ">y",
                },
                Package()
                {
                    // 0x1A SET_PIN_WIDGET_CONTROL 0x20
                    "Command", Buffer() { 0x01, 0xA7, 0x07, 0x20 },
                    "On Init", ">y",
                    "On Sleep", ">n",
                    "On Wake", ">y",
                },
                Package()
                {
                    // 0x21 SET_UNSOLICITED_ENABLE 0x83
                    "Command", Buffer() { 0x02, 0x17, 0x08, 0x83 },
                    "On Init", ">y",
                    "On Sleep", ">n",
                    "On Wake", ">y",
                }
            },
            "Perform Reset", ">n",
            "Perform Reset on External Wake", ">n", // enabled since using AppleALC
            "Send Delay", 10,
            "Sleep Nodes", ">n",
        },
    })
}
//EOF
````

-----
**Errors/Fixes**

Please report any issues or possible improvements to the guide and I will try my best to fix them asap.
  
-----  




 
### **Thanks to:**

RehabMan  
insanelydeepak  
People of the TonyMacx86 forum  
me for making this guide
