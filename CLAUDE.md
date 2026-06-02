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
