# Keyball44 ZMK config

## OS profile

Platform-dependent shortcuts are `#define`s in the "OS profile" block at the top of
`config/keyball44.keymap`. To switch OS, comment out the active block and uncomment the other.

| Define | Windows | macOS |
|--------|---------|-------|
| `OS_MOD(k)` | `LC(k)` | `LG(k)` |
| `K_COPY` | `LC(INSERT)` | `LG(C)` |
| `K_PASTE` | `LS(INSERT)` | `LG(V)` |
| `K_TAB_PREV` | `LC(LS(TAB))` | `LS(LG(LEFT_BRACKET))` |
| `K_TAB_NEXT` | `LC(TAB)` | `LS(LG(RIGHT_BRACKET))` |
| `K_SHOT` | `LG(LS(S))` | `LS(LG(NUMBER_4))` |
