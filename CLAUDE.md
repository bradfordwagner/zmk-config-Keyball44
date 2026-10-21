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

# OS chords (Windows / macOS)

Keymap-editor (nickcoutsos.github.io/keymap-editor) cannot parse preprocessor macros in bindings ("Could not parse keymap"). So OS chords are written inline in `config/keyball44.keymap` (Windows profile). No `OS_MOD`/`K_*` defines.

Switch table is in the comment block at the top of the keymap. To switch OS, replace every chord per that table, then commit, push, wait for CI, flash both halves (`/flash`), and test copy/paste, tab keys, screenshot key.

Rules:
- Never add function-like or binding macros. Write chords inline.
- Intentionally OS-independent: home-row GUI mods (S/F/J/L), X+C combo, right pinky, GM1 `LC(...)` tap-dances, ARROWS `LC(S)`.
