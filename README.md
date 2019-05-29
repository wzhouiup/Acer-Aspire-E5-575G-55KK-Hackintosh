# Acer-Aspire-E5-575G-55KK-Hackintosh
Hackintosh guide for the Acer E15 series E5-575G-55KK laptop

**Main Specs:** 
* Intel i5-7200u
* IGPU: Intel HD 620
  * DGPU: Nvidia 940mx 2GB (disabled)
* Realtek ALC255
* I2C keyboard

## Instructions:

**Important!**
Use the original Clover bootloader from https://sourceforge.net/projects/cloverefiboot/ when following [this laptop guide for UEFI.](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)

---
1. Follow the guide in order to create the bootable USB. For reference, the kexts I started off for the installation are as follows: 
  - FakeSMC
  - WhateverGreen
  - Lilu
  - RealtekRTL8111
  - VoodooPS2Controller

Use config_HD615_620_630_640_650.plist from the guide. I recommend using [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) if/when making changes to a .plist.

2.
