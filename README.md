# Kaiwa Vox

Browser control surface for Kraftor Kaiwa firmware and the **ATP3011R4-PU** AquesTalk pico LSI. GUI v1.0 — live phonetic speech over USB serial, MIDI voice shaping and slot playback, RAM/FRAM sentence banks, printable MIDI reference sheets, and Japanese-themed skins.

[Open the published app](https://deladriere.github.io/Kaiwa_Designer/)

## Features

- Speak AquesTalk ASCII phonetics over USB Serial at 115200 baud.
- Show board model, chip ID, and firmware version from `!INFO?`.
- Identify serial and MIDI when several Kraftor boards are connected.
- Shape the voice with Speed, Pitch, Accent, and Vowels (serial `!VOICE` + MIDI CC / pitch bend).
- Select MIDI channels 1–15 to match the board DIP switches.
- Edit RAM and FRAM sentence slots; bulk-fill from pasted text.
- Print RAM/FRAM MIDI reference sheets.
- Skins: Washi, Sumi, Matcha, Sakura, Torii.

## Requirements

- Chrome or Edge (Web Serial and Web MIDI).
- Kraftor board running Kaiwa firmware with an **ATP3011R4-PU** AquesTalk pico LSI.
- USB connection from the board to the computer.

## Text format

AquesTalk does **not** accept kanji, hiragana, or katakana. Enter romaji phonetics and end with `.` (max **127** ASCII bytes per phrase):

```text
konichiwa.
oha'yo-.
maka-/hannya-haramita-/si'n-gyo-.
```

Vowels (CC 3) inserts extra `-` after each lowercase `a e i o u` before speak — keep it at `0` for long phrases or they may return `!ERR too-long`.

Full symbol table, tips, and a Heart Sutra bank example are in the [user manual](user_manual.html#text-format). Datasheet: [atp3011_datasheet.pdf](https://www.a-quest.com/archive/manual/atp3011_datasheet.pdf).

## Usage

Open `index.html` in a supported browser (or use the published app link above).

**Serial = what** (phrase content):

1. Click `Select port` and choose the Kraftor USB serial device.
2. Confirm model / chip ID / `FW v…` in the header.
3. Click `Identify Serial` to hear `si-riaru.` on that port.
4. Type phonetics and click `Speak` (or press Enter).

**MIDI = how and when** (voice + triggers):

1. Click `Connect MIDI` and select the output.
2. Set channel 1–15 to match the board DIP switches.
3. Click `Identify MIDI` (needs serial + MIDI): writes `mi-di.` to RAM slot 0, then sends note 28.
4. Move the voice dials, or play notes to trigger stored slots.

| MIDI | Result |
| --- | --- |
| Notes 28–47 | Play RAM slots 0–19 |
| Notes 48–127 | Play FRAM slots 0–79 |
| CC 1 | Speed (50–300) |
| Pitch bend | Pitch register (bend up = higher voice) |
| CC 2 | Accent (0–255) |
| CC 3 | Vowel elongation (0–6) |

DIP switches are read at startup. DIP1=8, DIP2=4, DIP3=2, DIP4=1. All OFF = Omni. Full table: [user manual](user_manual.html#midi-dip-switches).

Chrome does not reliably pair a Web Serial port with a Web MIDI output — use the identify buttons when several boards are connected.

## Manual

The [user manual](user_manual.html) covers text format, serial/MIDI workflow, voice controls, DIP switches, banks, and useful `!` commands.

## Project structure

- `index.html` — Kaiwa Vox GUI
- `user_manual.html` — browser-readable manual
- `assets/` — optional images for this README
