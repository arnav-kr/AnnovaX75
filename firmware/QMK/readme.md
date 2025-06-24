# Annova X75 Rev 1

![annova/x75/rev1](/renders/0.png)

A 75% Mechanical Keyboard, custom built from scratch.

* Keyboard Maintainer: [Arnav Kumar](https://github.com/arnav-kr)
* Hardware Supported: RP2040
* Hardware Source: [arnav-kr/annovaX75](https://github.com/arnav-kr/annovaX75)

Make example for this keyboard (after setting up your build environment):

    make annova/x75/rev1:default

Flashing example for this keyboard:

    make annova/x75/rev1:default:flash

See the [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) and the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information. Brand new to QMK? Start with our [Complete Newbs Guide](https://docs.qmk.fm/#/newbs).

## Bootloader

Enter the bootloader in 3 ways:

* **Bootmagic reset**: Hold down the key at (0,0) in the matrix (usually the top left key or Escape) and plug in the keyboard
* **Physical reset button**: Briefly press the button on the back of the PCB - some may have pads you must short instead
* **Keycode in layout**: Press the key mapped to `QK_BOOT` if it is available
