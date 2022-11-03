# 3DP-Marlin 3D Printer Firmware
<img align="right" src="https://pbs.twimg.com/profile_images/529294269639438338/xHCyEu2x.jpeg" />

  * [Configuration & Compilation](/Documentation/Compilation.md)
  * Supported
    * [Features](/Documentation/Features.md)
    * [Hardware](/Documentation/Hardware.md)
    * [GCodes](/Documentation/GCodes.md)
  * Notes
    * [Auto Bed Leveling](/Documentation/BedLeveling.md)
    * [Filament Sensor](/Documentation/FilamentSensor.md)
    * [Ramps Servo Power](/Documentation/RampsServoPower.md)

##### [RepRap.org Wiki Page](http://reprap.org/wiki/Marlin)

## Quick Information

This is a modification of the [Marlin Firmware](https://github.com/MarlinFirmware/Marlin), it is configured for the [3DP1000](http://3dpunlimited.com/printer-options-specifications/) which uses the [RAMPS 1.4 Ultimate POWER Kit](http://www.reprapdiscount.com/home/29-ramps-14-ultimate-power-kit-1-wiring-set-capable-of-24v.html).

[3DP1000X1](https://github.com/3DP-Unlimited/3DP-Marlin/tree/3DP1000X1) is the single extruder branch and [3DP1000X2](https://github.com/3DP-Unlimited/3DP-Marlin/tree/3DP1000X2) is the dual extruder branch.

## Additional Features
 - [G5 X Y Z](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L1483) can be used to babystep the machine and **attemps** to prevent endstop crashes, the argument is in steps and the equivalent distance is computed and displayed.
 - Modified the add_homing[Z_AXIS] element (from M206) to store the babystepped Z axis offsets and reproduce them [when homing](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L1813), the babystepped Z offset can be saved to the EEPROM using M500 or "Store memory" on an LCD controller, use M206 Z0 or "Set home offsets" at Z=0 on an LCD controller to clear the offset.
 - [M19 Z](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L2103) (and LCD menu) can be used to resume a print from either a given Z argument or the current Z height (used with no arguments), uses an [algorithm](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/planner.cpp#L547) to attempt to learn of any hops (downward Z motion) during parsing and tries to account for it, this is a heavily modified feature from [Vince's Solidoodle Marlin Code](http://www.soliforum.com/topic/5971/firmware-mods-to-rescue-and-resume-failed-prints/).
 - Attemps to [predict the current layer](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/planner.cpp#L597) and display it on an LCD display under Main Menu > Tune > [Layer](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/ultralcd.cpp#L463) and displays it with [M114](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L2939).
 - Includes a filament alarm trigger using a simple microswitch [(M600)](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L1418), [commented code](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L420) is included for using a [rotary encoder](https://www.sparkfun.com/products/10790) as a filament feed sensor (pin change ISR).
 - Can resume the print from a filament alarm by sending an [M601](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L785) code.
 - The hotend will now cool down and the piezoelectric speaker will quite down after [30 min](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/Marlin_main.cpp#L3834) of being in the filament alarm mode (and will resume normally).
 - Extruder offsets can be [set from an LCD controller](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/ultralcd.cpp#L904) and [saved to the nonvolatile EEPROM memory](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/ConfigurationStore.cpp#L70) in [3DP1000X2](https://github.com/3DP-Unlimited/3DP-Marlin/tree/3DP1000X2).
 - There is a [menu item](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/ultralcd.cpp#L713) to extrude from a second extruder in [3DP1000X2](https://github.com/3DP-Unlimited/3DP-Marlin/tree/3DP1000X2).
 - Thermal runaway now [responds as it should](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/temperature.cpp#L1107); it can potentially prevent fires, or at the least, nozzle wear.
 - Added an [LED indication function](https://github.com/3DP-Unlimited/3DP-Marlin/blob/3DP1000X2/Marlin/temperature.cpp#L178) which [warns](http://www.dialight.com/Assets/Brochures_And_Catalogs/Indication/MDEL657DF001.pdf) that the bed is approaching, or has reached 70°C; used for CE compliance in conjunction with the 3DP1000's bed [temperature controller](http://www.brewmart.com.au/brewmart-shop/PDF/ITEMS/18704-ed330.pdf) system.

## Contact

**3DP Unlimited Support:**

support@3dpunlimited.com

**General Marlin Support:**

__IRC:__ #marlin-firmware @freenode ([WebChat Client](https://webchat.freenode.net/?channels=marlin-firmware))

__Mailing List:__ marlin@lists.0l.de ([Subscribe](http://lists.0l.de/mailman/listinfo/marlin), [Archive](http://lists.0l.de/pipermail/marlin/))

## Credits

The current 3D Platform dev team consists of:

 - Ben Williams
 - Joe Binka




The original authors and main contributors of Marlin are:
  - Erik van der Zalm ([@ErikZalm](https://github.com/ErikZalm))
  - [@daid](https://github.com/daid)

## License

3DP-Marlin is published under the [GPL license](/Documentation/COPYING.md) because I (we) believe in open development.
Please do not use this code in products (3D printers, CNC etc) that are closed source or are crippled by a patent.

[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=ErikZalm&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)
