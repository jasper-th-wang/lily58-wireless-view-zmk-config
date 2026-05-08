**need to format**
# Note to self

Remember to go on ZMK studio and do RESET, so the ZMK Studio's custom setting won't override the config file I flashed

when flashing firmware, you have to do it one side at a time. And you should use bootloader key for left side when you are doing left side. and use bootloader key for the right side when you are doing the right.

When flashing you the terminal like cp /Users/jasperwang/Downloads/firmware-2/lily58_left\ nice_view_adapter\ nice_view-nice_nano_v2-zmk.uf2 /Volumes/NICENANO
this is because if you copy directly via Finder .DS_Store file may cause some issues my MacOS (my guess, cuz it didnt work.)

Don't skip any layers: see commit 6854c8a, I had an status: reserved layer before another layer I would like to enter, that messes things up

# links
https://zmk.dev/docs/keymaps/list-of-keycodes
https://zmk.dev/docs/features/split-keyboards
steps of flashing: https://zmk.dev/docs/user-setup#install-the-firmware
