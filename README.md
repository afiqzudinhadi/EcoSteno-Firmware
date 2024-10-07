# EcoSteno Custom Keymaps

This repository contains the custom keymaps for the EcoSteno keyboard. It also contains the guide on how to set up the keymaps.

# Table of Contents

- [EcoSteno Custom Keymaps](#ecosteno-custom-keymaps)
- [Table of Contents](#table-of-contents)
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
  - [Issues](#issues)
    - [Bootloader not found](#bootloader-not-found)

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

## 1. Prepare Build Environment

```bash
brew install qmk/qmk/qmk
```

## 2. Run QMK Setup

```bash
qmk setup
```

Answer `Y` to all the prompts.

## 3. Copy the keyboard to the QMK directory

```bash
cp -r keyboards/* ~/qmk_firmware/keyboards/
```

## 4. Test Build Environment

```bash
qmk compile -kb noll/ecosteno -km default
```

# Remapping Keys

## 1. Edit the Keymap File

Keymaps are located in the following directory:

```bash
keyboards/noll/ecosteno/keymaps/default/keymap.c
```

Keymap guide can be found [here](https://docs.qmk.fm/keycodes_basic).

## 2. Copy the Keymap to the QMK Directory

If keymap file is edited, copy the keymap to the QMK directory:

```bash
cp -r keyboards/* ~/qmk_firmware/keyboards/
```

## 3. Compile the Keymap

```bash
qmk compile -kb noll/ecosteno -km default
```

# Flashing the Keyboard

1. Plug in the keyboard to the computer.
2. Press the reset button on the back of the keyboard near the USB port.
   1. LEDs on the keyboard will turn off.
3. Run the following command to flash the keyboard:

```bash
qmk flash -kb noll/ecosteno -km default
```

4. The keyboard will restart and the new keymap will be loaded.
   1. LEDs on the keyboard will turn on.

## Issues

### Bootloader not found

```bash
Bootloader not found. Make sure the board is in bootloader mode. See https://docs.qmk.fm/#/newbs_flashing
Trying again every 0.5s (Ctrl+C to cancel)...
```

1. Run the following command:

```bash
qmk doctor
```

2. Flash the keyboard again.
