# MultiToo

Atari launcher for Nintendo DS homebrew (R4 Gold, Twilight++ / nds-bootstrap setups).
Home screen with four touch tiles: **Atari 2600, 2600 Junior, 5200, 7800**.
Browse ROMs, pick one, and MultiToo launches it in the right emulator.

> Status: written but **not compiled or run** by the author of this file.
> Expect to fix a typo or two on first build.

## Build

1. Install devkitPro with `nds-dev` (devkitARM, libnds, libfat).
2. Get two files from https://github.com/DS-Homebrew/nds-hb-menu (the loader MultiToo uses to start other .nds files):
   - `arm9/source/nds_loader_arm9.c` and `arm9/source/nds_loader_arm9.h`  -> copy to `source/`
   - build its `bootloader/` folder to get `load.bin`                      -> copy to `data/load.bin`
3. `make`  ->  `MultiToo.nds`

## Install on the card

```
/MultiToo.nds
/emulators/StellaDS.nds     (2600 + Junior)   by wavemotion
/emulators/A5200DS.nds      (5200)            by wavemotion
/emulators/A7800DS.nds      (7800)            by wavemotion
/roms/...                   any subfolders, up to 6 deep
```

Emulators are looked for in `/emulators/`, `/emu/`, `/_nds/`, then the card root.
Patch MultiToo.nds with DLDI for your card (Twilight++ does this automatically).

## ROM detection

| Extension | Console |
|-----------|---------|
| .a26      | 2600 (Junior if the path contains `2600jr` or `junior`) |
| .a52      | 5200 |
| .a78      | 7800 |
| .jr       | 2600 Junior |
| .bin      | 2600 by default; 5200 / 7800 / Junior if a folder name contains `5200` / `7800` / `2600jr` |

## Controls

Home: D-pad or tap to choose, A or tap to open, Y rescans.
List: Up/Down scroll, L/R page, A or double-tap to play, B or tap footer to go back.

## Known uncertainties

- The emulators must accept a ROM path as `argv[1]` when launched. Stella DS / A5200DS / A7800DS
  support hbmenu-style argv launching in recent versions, but check yours.
- 2600 Junior runs on the Stella DS core (identical hardware); the tile is a library/sorting category.
- Atari emulators are GPL; if you redistribute a bundle, include source.
- No ROMs or BIOS files are included. The 5200 and 7800 emulators need their own BIOS files in the folders their docs specify.
