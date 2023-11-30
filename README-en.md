# My 3DP Configs
[![Build Status](https://github.com/macdylan/3dp-configs/actions/workflows/pack.yml/badge.svg)]
[Chinese Readme](./README.md)

The unofficial PrusaSlicer and OrcaSlicer print settings provided are personally calibrated by me. Please read the README file in the subdirectory carefully for proper configuration. If you encounter any printing errors, kindly post an issue. Thank you.

> Due to limitations in tested materials and variations in printing environments, it is essential to perform print validation and filament calibration before use.

## How to use

Download [Releases](https://github.com/macdylan/3dp-configs/releases)

I will regularly update them. Since they are unofficial configuration files, they cannot be automatically updated within the slicer software. Please manually download and install them.
Additionally, I am actively reaching out to the maintainers of these projects to expedite their inclusion in the official software release.

### PrusaSlicer

- Open PrusaSlicer and click on the `Help` menu / `Show Configuration Folder`
- Extract the files from zip file and copy all of them to the `vendor` directory. If the destination files already exist, choose to overwrite them.
- Restart PrusaSlicer and click on the `Configuration` menu / `Configuration Assistant (or Wizard)`
- Select Snapmaker from the "Other Vendors" section, click Next, choose the desired printer and filament, then complete the setup.

### OrcaSlicer
> Please note that if you are using the Snapmaker parameters from the official release and have saved modified settings, they will disappear (not lost, as they will still be saved in your personal folder but will not be displayed in the menu).

- Open OrcaSlicer and remove the previously configured Snapmaker device under "Printer" then close the software.
- Navigate to the program installation directory:
  - macOS: /Applications/OrcaSlicer.app/Contents/Resources/profiles/
  - Windows: (locate where the program is installed)/profiles/
- Extract the files from zip file and copy all of them into the directory, choosing to overwrite existing files.
- Restart OrcaSlicer, add the Snapmaker printers under "Printer" and add all the new Snapmaker filaments under "Filament", Your setup is now complete.

### How to send the gcode file to Snapmaker printers via WiFi

Use my other project [sm2uploader](https://github.com/macdylan/sm2uploader), which simulates the API of OctoPrint, you can utilize the physical printer connection feature within the slicer software to send Gcode files to the Snapmaker printer through sm2uploader.

<img width="701" src="./_assets/3.png">
<br />
<img width="701" src="./_assets/4.png">

## Explanation for Start GCodes
In the version dated 20231130, I've added some logic to clean the nozzle. Here are the complete steps:

1. Start with the first layer bed temperature, preheat the nozzle to 165 degrees, and move the nozzle to a position that's convenient for manual cleaning. You can check the nozzle area for any debris and clean it with a wire brush or other tools.
2. Once the bed reaches the target temperature, the nozzle will home. With Snapmaker 2, it will circle around the bed at a height of 0.2mm for a structure check, You can observe if the bed is mostly level and also see the boundaries of the nozzle's movement, which are reduced when using the Dual Extruder Module and Quick Swap Kit. With J1, will only flash the LED to signal that the print head is about to home, no other actions.
3. The nozzle then moves away from the bed and heats up to 15 degrees above the printing temperature. The purpose is to prevent clogging from any high-temperature material residue in the nozzle which could prevent extrusion. Please note that temperature is based on my experience, if you encounter a clogged nozzle, please report the issue.
4. Flush the filament at two different temperatures to ensure a clean nozzle, using about 4-8cm of filament, which isn't wasteful considering the reliability of the printing process. If you want to avoid any waste, you can disable this logic in the gcode with `{if 0 == 1}...{endif}`.
5. For dual extrusion module or J1 dual material printing, the standby nozzle is flushed first, followed by the initial printing nozzle. This is to prevent any material loading errors or nozzle malfunctions during the actual print, any pre-checks are helpful.
6. After flushing, an L-shaped thin line is extruded at the bed edge to remove any residual material around the nozzle, which helps improve print quality.
7. Start the printing process.
8. At the end of printing, retract the filament back near the extruder gear. This way, even after cooling down, you can easily change the filament without cut or heat.

Some logic will differ depending on the type of device. If you like my works, please show your support by clicking the star in the top right on GitHub. Or you can buy me a coffee: https://ko-fi.com/L3L1MFQF6
