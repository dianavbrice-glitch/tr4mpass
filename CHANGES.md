# Changelog

All notable changes to this project will be documented in this file.

## Unreleased

- usb_dfu: fallback to descriptor index 4 when index 3 is generic — ensures DFU serial parsing reads `CPID`/`ECID` from devices that expose the detailed serial at descriptor index 4.
