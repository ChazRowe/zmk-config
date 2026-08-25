# Allium58 nice!view status screen

This local shield exposes the nice!view status-screen implementation used by
the Allium58 builds so it can be customized and version-controlled with the
keyboard configuration.

The implementation was copied without behavioral changes from ZMK's
`boards/shields/nice_view` shield at ZMK `v0.3` commit
`edf5c0814fd3ea202e43aad2d68fd32e882a518c`. The local shield and widget
configuration symbols were renamed from `NICE_VIEW` to `ALLIUM_VIEW` to avoid
colliding with the upstream shield.

The central/left display is implemented by `widgets/status.c`. The
peripheral/right display is implemented by `widgets/peripheral_status.c` and
uses the artwork compiled in `widgets/art.c`. Shared drawing helpers live in
`widgets/util.c` and `widgets/bolt.c`. `custom_status_screen.c` creates the
screen and attaches the appropriate widget for each half.

Both firmware targets select this shield after `nice_view_adapter`; the
upstream ZMK source remains an external build dependency.

The battery bars are deliberately conservative: the lowest 25% reported by
ZMK is reserved, so a measured level of 25% or less is drawn as empty. Adjust
`DISPLAY_BATTERY_RESERVE_PERCENT` in `widgets/util.c` to change the reserve.
