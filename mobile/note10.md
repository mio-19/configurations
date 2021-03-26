# Usage

+ Google Apps
+ KVM (LimboPC, Windows 10 on ARM) https://github.com/limboemu/limbo/wiki/KVM
+ Taking down notes
+ Minecraft Java edition https://github.com/AOF-Dev/MCinaBox

# Procedure

1. flash stock ROM (disable auto reboot)
1. press volume down + power to reboot. hold volume up + volume down for returning to flash
1. flash TWRP. hold volume up + power to boot into TWRP
1. wipe data & cache
1. flash ~modified~ multi-disabler
1. flash ThundeRStormS
1. boot into system

## TWRP

https://forum.xda-developers.com/t/recovery-official-3-5-0-x-twrp-for-galaxy-note-10-5g-exynos.4198409/

### multi-disabler

https://forum.xda-developers.com/t/pie-10-11-system-as-root-multidisabler-disables-encryption-vaultkeeper-auto-flash-of-stock-recovery-proca-wsm-cass-etc.3919714/
https://github.com/ianmacd/multidisabler-samsung/commit/df9e06eecfc6c3c64e7d17c9552180aba1ed0ee6

#### Modify:

Remove "Disable FBE" (Encrypt)

https://github.com/ianmacd/multidisabler-samsung/blob/df9e06eecfc6c3c64e7d17c9552180aba1ed0ee6/META-INF/com/google/android/update-binary

remove `disable_fbe`

## Kernel

ThundeRStormS

https://forum.xda-developers.com/t/kernel-thunderstorms-kernel-for-samsung-galaxy-s10-n10-family-only-exynos.4154863/
https://github.com/ThunderStorms21th/Galaxy-S10

Useful Features: Magisk
