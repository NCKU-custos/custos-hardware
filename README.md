# custos-hardware

Generic Pixhawk parameter sets, calibration procedures, and airframe configuration templates for the Custos drone stack.

## Scope

This repo intentionally contains **only generic, non-identifying** configuration:

- Airframe templates (frame geometry, mass properties, motor maps)
- Default Pixhawk parameter sets per airframe class
- Calibration *procedures* (documentation), not calibration *results*

Per-physical-drone data (serial-tagged calibration, fleet inventory) lives outside git. See [ADR 0013](https://github.com/NCKU-custos/custos-bringup/blob/main/docs/adr/0013-public-from-day-one.md) for the public-data boundary.

For the system overview, see [`custos-bringup`](https://github.com/NCKU-custos/custos-bringup).
