# EcoSteno Custom Keymaps

This repository contains the custom keymaps for the EcoSteno keyboard. It also contains the guide on how to set up the keymaps.

# Table of Contents

- [EcoSteno Custom Keymaps](#ecosteno-custom-keymaps)
- [Table of Contents](#table-of-contents)
- [Hardware Info](#hardware-info)
- [Current Keymap](#current-keymap)
- [Related Articles](#related-articles)
- [Pre-requisites](#pre-requisites)
- [Clone Repository](#clone-repository)
- [Set Up QMK Environment](#set-up-qmk-environment)
    - [1. Prepare Build Environment](#1-prepare-build-environment)
    - [2. Run QMK Setup](#2-run-qmk-setup)
    - [3. Copy the keyboard to the QMK directory](#3-copy-the-keyboard-to-the-qmk-directory)
    - [4. Test Build Environment](#4-test-build-environment)
- [Remapping Keys](#remapping-keys)
    - [1. Edit the Keymap File](#1-edit-the-keymap-file)
    - [2. Copy the Keymap to the QMK Directory](#2-copy-the-keymap-to-the-qmk-directory)
    - [3. Compile the Keymap](#3-compile-the-keymap)
- [Flashing the Keyboard](#flashing-the-keyboard)
    - [1. Plug in the keyboard](#1-plug-in-the-keyboard)
    - [2. Press the reset button](#2-press-the-reset-button)
    - [3. Flash the keyboard](#3-flash-the-keyboard)
    - [4. Check the keyboard](#4-check-the-keyboard)
  - [Issues](#issues)
    - [Bootloader not found](#bootloader-not-found)
  - [Fixes](#fixes)
    - [1. Run QMK Doctor](#1-run-qmk-doctor)
    - [2. Flash the keyboard again](#2-flash-the-keyboard-again)

# Hardware Info

| Property | Value |
|----------|-------|
| Keyboard | EcoSteno |
| Keys | 28 (2 top + 12+12 main + 4 thumbs) |
| MCU | STM32F103 |
| Firmware | QMK |
| Bootloader | stm32duino |
| Connection | USB |
| USB Vendor ID | `0xFEED` |
| USB Product ID | `0x3621` |
| Device Version | `1.1.2` |
| Manufacturer | Noll Electronics LLC |
| Steno Protocol | GeminiPR |
| LEDs | Red (GPIOA 0), Green (GPIOA 1) |

# Current Keymap

Key positions reference:
```
        0        1                    2        3
 4  5   6   7   8   9  | 10  11  12  13  14  15
16 17  18  19  20  21  | 22  23  24  25  26  27
                28  29  | 30  31
```

### Layer 0: STENO (Plover / GeminiPR)
```
           #2         #4                       #8         #0
->QWRT  S  T  P  H  *  |  *  F  P  L  T  D
  _     S  K  W  R  *  |  *  R  B  G  S  Z
                A  O   |  E  U

LED: green on, red off
```

### Layer 1: QWERTY
```
          TAB       ESC                    ENTER      BSPC
LSHFT  Q  W  E  R  T  |  Y  U  I  O  P    '
[L1]   Z  X  C  V  B  |  N  M  ,  .  /    [CAPS]
              CTRL GUI | SPC  ALT

LED: red on, green off

Combos (QWERTY + QWERTY_CAPS):
  top+bottom row same col = virtual home row:
    Q+Z=A  W+X=S  E+C=D  R+V=F  T+B=G  Y+N=H  U+M=J  I+,=K  O+.=L  P+/=;
  top row + modifier key = numbers:
    Q+TAB=1  W+TAB=2  E+ESC=3  R+ESC=4  T+ESC=5
    Y+ENT=6  U+ENT=7  I+ENT=8  O+BSP=9  P+BSP=0
  CAPS layer: same combos produce shifted output (! @ # $ % ^ & * ( ) :)
[L1] = hold opens LAYER1
[CAPS] = hold activates QWERTY_CAPS (shifted combos)
```

### Layer 2: QWERTY_CAPS (shift layer)
```
         S(TAB)    S(ESC)                S(ENTER)   S(BSPC)
LSHFT  Q  W  E  R  T  |  Y  U  I  O  P    "
[L1]   Z  X  C  V  B  |  N  M  <  >  ?    _
              CTRL GUI | SPC  ALT

All alpha/symbol keys output shifted versions.
LED: red on, green off
```

### Layer 3: LAYER1 (nav/symbols)
```
            TAB       ESC                       ENTER      BSPC
->STEN  `  _  _  \  VOL+  |  +   [   UP    ]    *     =
  _     Z  X  C  V  VOL-  |  -  LEFT DOWN RIGHT /   RSHFT
               CTRL  GUI  | SPC  ALT

LED: both red and green on
->STEN = switch to STENO layer
```

# Related Articles

- [QMK Firmware Guide](https://docs.qmk.fm/newbs)
- [Default EcoSteno Firmware by Nolltronics](https://github.com/nkotech/EcoSteno-Firmware)

# Pre-requisites

- EcoSteno Keyboard
- MacOS
- [Homebrew](https://brew.sh/)
- This Repository - [Custom EcoSteno Keymap](https://github.com/afiqzudinhadi/EcoSteno-Firmware)

# Clone Repository

```bash
git clone git@github.com:afiqzudinhadi/EcoSteno-Firmware.git
```

# Set Up QMK Environment

### 1. Prepare Build Environment

```bash
brew install qmk/qmk/qmk
```

### 2. Run QMK Setup

```bash
qmk setup
```

Answer `Y` to all the prompts.

### 3. Copy the keyboard to the QMK directory

```bash
cp -r keyboards/* ~/qmk_firmware/keyboards/
```

### 4. Test Build Environment

```bash
qmk compile -kb noll/ecosteno -km default
```

# Remapping Keys

### 1. Edit the Keymap File

Keymaps are located in the following directory:

```bash
keyboards/noll/ecosteno/keymaps/default/keymap.c
```

Keymap guide can be found [here](https://docs.qmk.fm/keycodes_basic).

### 2. Copy the Keymap to the QMK Directory

If keymap file is edited, copy the keymap to the QMK directory:

```bash
cp -r keyboards/* ~/qmk_firmware/keyboards/
```

### 3. Compile the Keymap

```bash
qmk compile -kb noll/ecosteno -km default
```

# Flashing the Keyboard

### 1. Plug in the keyboard

### 2. Press the reset button

- The button is on the back of the keyboard near the USB port.
- LEDs on the keyboard will turn off.

### 3. Flash the keyboard

Run the following command to flash the keyboard:

```bash
qmk flash -kb noll/ecosteno -km default
```

### 4. Check the keyboard

- The keyboard will restart and the new keymap will be loaded.
- LEDs on the keyboard will turn on.

## Issues

### Bootloader not found

```bash
Bootloader not found. Make sure the board is in bootloader mode. See https://docs.qmk.fm/#/newbs_flashing
Trying again every 0.5s (Ctrl+C to cancel)...
```

## Fixes

### 1. Run QMK Doctor

```bash
qmk doctor
```

### 2. Flash the keyboard again
