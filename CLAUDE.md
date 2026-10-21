# PMW3610 RUN/REST Range Validation

Before applying any RUN or REST mode change, verify every affected value is within the driver's acceptable range. Setting an out-of-range value breaks sensor init and the trackball stops working entirely.

Formulas from `pmw3610.c`:

| Setting | Min | Max |
|---------|-----|-----|
| RUN downshift | 13ms | 3,264ms |
| REST1 sample | 10ms | 2,550ms |
| REST1 downshift | `16 × REST1_SAMPLE_TIME_MS` | `255 × 16 × REST1_SAMPLE_TIME_MS` |
| REST2 sample | 10ms | 2,550ms |
| REST2 downshift | `128 × REST2_SAMPLE_TIME_MS` | `255 × 128 × REST2_SAMPLE_TIME_MS` |

Changing a sample time also changes the valid range for its downshift — always recalculate both together.

# OS profile (Windows / macOS)

`config/keyball44.keymap` has an "OS profile" `#define` block at the top. It is a preprocessor switch, not a Kconfig or build flag. One block is active, the other is commented out. Switching OS means swapping which block is commented.

Defines: `OS_MOD(k)`, `K_COPY`, `K_PASTE`, `K_TAB_PREV`, `K_TAB_NEXT`, `K_SHOT`. Values are in `README.md`.

Use sites:
- `K_COPY` / `K_PASTE`: `copy_paste` tap-dance (copy on tap, paste on double-tap). Windows uses Ctrl+Insert / Shift+Insert so it works in terminals and browsers.
- `OS_MOD`: `tab_refresh` combo (R), MOUSE and SCROLL layers (R, W).
- `K_TAB_PREV` / `K_TAB_NEXT`: `tab_prev` / `tab_next` combos, MOUSE and SCROLL layers, PAREN layer (next only).
- `K_SHOT`: MOUSE and SCROLL layers, top-left key.

Rules:
- New OS-dependent chord: add a define in both blocks and use it. Never hard-code `LG(...)` or `LC(...)` for a shortcut that differs per OS.
- Intentionally not parameterized: home-row GUI mods (S/F/J/L), the X+C combo, the right pinky, GM1 game tap-dances (`LC(...)`), ARROWS `LC(S)`. They are finger-position or OS-independent choices.
