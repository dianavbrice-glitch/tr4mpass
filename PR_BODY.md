Title: usb_dfu: fallback to descriptor index 4 when index 3 is generic

Summary:

Some Apple DFU devices expose the detailed DFU serial (containing `CPID`/`ECID`) at USB string descriptor index 4 instead of index 3. This change adds a safe fallback to read descriptor index 4 when index 3 contains the generic product string (e.g., "Apple Mobile Device (DFU Mode)").

Changes:
- `src/device/usb_dfu.c`: attempt descriptor index 3, if it appears generic then try index 4 and parse `CPID`/`ECID`.

Testing:
1. Build the project and run unit tests: `make && make test`.
2. With an Apple DFU device attached (via `usbipd` into WSL), run: `./tr4mpass --detect-only --verbose` and confirm output includes `CPID` and `ECID`.
3. Confirm existing unit tests still pass.

Notes:
- This is a minimal, targeted fix that does not change bypass behavior. It only improves DFU serial parsing robustness.
