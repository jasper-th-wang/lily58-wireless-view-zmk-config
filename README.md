# Steps to Update Config

1. Edit `./config/lily58.keymap`.
2. Commit and push — this will trigger the build GitHub Action.
3. On the workflow run page, click **Summary**, then scroll to the bottom to download the firmware.
4. Plug in the **left** keyboard and press the bootloader key. You should see a `NICENANO` device mounted.
5. Use the following command to copy the firmware to the left side:
```bash
   cp ~/Downloads/firmware/lily58_left\ nice_view_adapter\ nice_view-nice_nano_v2-zmk.uf2 /Volumes/NICENANO
```
6. While still plugged in, test the left side before unplugging to avoid Bluetooth issues.
7. Repeat steps 4–6 for the **right** side (using the right-side `.uf2` file).
8. Done.

# Notes to Self

- Remember to go to ZMK Studio and *restore defaults* so that ZMK Studio's custom settings won't override the config file you flashed.
- When flashing firmware, do it **one side at a time**. Use the bootloader key on the left side when flashing the left side, and the bootloader key on the right side when flashing the right side.
- Flash via the terminal rather than Finder, e.g.:
  ```bash
  cp /Users/jasperwang/Downloads/firmware-2/lily58_left\ nice_view_adapter\ nice_view-nice_nano_v2-zmk.uf2 /Volumes/NICENANO
  ```
  Copying directly through Finder on macOS can create a `.DS_Store` file that seems to cause issues (this is my guess, since it didn't work for me).
- **Don't skip any layers.** See commit `6854c8a`: I had a `status: reserved` layer before a layer I wanted to enter, and it messed things up.

# Helpful Links

- [List of keycodes](https://zmk.dev/docs/keymaps/list-of-keycodes)
- [Split keyboards](https://zmk.dev/docs/features/split-keyboards)
- [Steps for flashing firmware](https://zmk.dev/docs/user-setup#install-the-firmware)

# Abandoned

## Mouse Support

I considered enabling mouse support, but the [ZMK mouse emulation docs](https://zmk.dev/docs/keymaps/behaviors/mouse-emulation) note:

> **Refreshing the HID Descriptor**
>
> Enabling or disabling the mouse emulation feature modifies the HID report descriptor and requires it to be refreshed. The mouse functionality will not work over BLE until that is done.

This seems pretty involved. From the docs:

> **Refreshing the HID Descriptor**
>
> Enabling certain features or behaviors in ZMK changes the data structure that ZMK sends over USB or BLE to host devices. This in turn requires HID report descriptors to be modified for the reports to be parsed correctly. Firmware changes that would modify the descriptor include the following:
>
> - Changing any of the settings under the HID category, including enabling/disabling NKRO or HID indicators
> - Enabling mouse features, such as adding mouse keys to your keymap
>
> While the descriptor refresh happens on boot for USB, hosts will frequently cache this descriptor for BLE devices. In order to refresh this cache, you need to remove the keyboard from the host device, clear the profile associated with the host on the keyboard, then pair again. For Windows systems you might need to follow the additional instructions in the section on troubleshooting connection issues.
