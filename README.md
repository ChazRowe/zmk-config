# Chaz's Wireless Allium58

ZMK user configuration for a BeeKeeb Wireless Allium58 MX with two
nice!nano v2 controllers and two Memory-in-Pixel (`nice!view`) displays.
The Allium58 uses ZMK's in-tree Lily58 shield because the two boards share
the same key layout and wiring.

## Layout

The typing grid comes from `keyboards/planck/keymaps/chaz` in
`ChazRowe/qmk_firmware`. Its four Planck rows are shifted onto the top four
physical rows of the Lily58; the eight low-profile thumb keys are macros,
not typing keys.

- Dvorak is the firmware default. QWERTY, Colemak, and Dvorak can be selected
  from Adjust and the choice is saved in the nice!nano's nonvolatile flash.
- Lower and Raise retain the Planck symbol, function, and navigation maps.
- Holding the left Space key opens Numpad; tapping it sends Space.
- Holding Lower and Raise together opens Adjust. Bluetooth controls live
  there so Lower remains fully available.
- The right edge has `Right Shift`/`Enter` and `Right Ctrl`/`Right Arrow`
  dual-role keys.
- Both keys below the displays hold
  `Left Shift+Left Ctrl+Left GUI+Left Alt+Right Alt+Right Shift` as a Meta
  chord.
- The eight low-profile keys emit that Meta chord plus F1 through F8,
  from left to right.

The full, position-by-position map is documented beside the bindings in
[`config/lily58.keymap`](config/lily58.keymap).

## Building and flashing

Every push runs GitHub Actions. Open the newest successful **Build ZMK
firmware** run, download its `firmware` artifact, and unzip it. It contains:

- `allium58_left_niceview.uf2`
- `allium58_right_niceview.uf2`
- `settings_reset.uf2` (recovery only)

To flash one half, connect it over USB, double-tap that half's physical reset
button, and wait for the nice!nano bootloader drive to appear. Copy the UF2
for that half to the root of the drive. It will unmount and reboot itself.
Flash the right UF2 to the right half and the left UF2 to the left half.

The left half is the split central: it advertises to the computer and runs
the keymap. The right half is a peripheral and talks only to the left half.
After both have rebooted, pair the host with **Allium58**.

On Adjust, the first key clears the current Bluetooth profile and the next
five keys select profiles 1 through 5. If pairing becomes confused, forget
Allium58 on the host, clear the selected keyboard profile, and pair again.

`settings_reset.uf2` is a last-resort recovery image. Flash it to each half,
then immediately flash the correct normal UF2 to each half again. It erases
split bonds, host Bluetooth profiles, and the saved base-layout selection.
