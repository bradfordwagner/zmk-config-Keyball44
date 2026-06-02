Read config/boards/shields/keyball_nano/keyball44_right.conf and extract the current PMW3610 REST mode settings, then output a table with these columns:

| Mode | Sample period | Polling rate | Poll interval | Idle before stepping down |

Rows to include: RUN, REST1, REST2, REST3.

- Sample period and Poll interval are the same value (in ms).
- Polling rate is 1000 / sample_period in Hz.
- "Idle before stepping down" is the downshift time in ms with a human-readable approximation in parentheses.
- For REST3, use "default" for sample period/rate and "—" for idle time since no downshift is configured.
- For RUN, the sample period is always 4ms (250Hz) and the downshift time is CONFIG_PMW3610_RUN_DOWNSHIFT_TIME_MS.
