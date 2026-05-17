# custos-hardware — CLAUDE.md

Generic Pixhawk parameter sets, calibration procedures, and airframe configuration templates for the Custos drone stack. **Data and configuration only.** No compile units.

Workspace-wide rules and state caveats live at `../CLAUDE.md` (= `/space/drone/CLAUDE.md`). If you are in a standalone clone, the one rule below is the one most likely to be violated when working in this repo.

## The one rule

**Generic configurations only. No per-physical-drone data.** Calibration *procedures* (how to do it) are welcome here; calibration *results* (the numbers from a specific drone's IMU run) are not. Anything that identifies a specific airframe by serial number, paint scheme, fleet ID, owner, location, or other distinguishing mark belongs outside git in a private inventory system. This repo is public (ADR 0013); committing identifying data here is irreversible.

## State of this repo

- Single package: `custos_hardware_airframes` (`package.xml`, `CMakeLists.txt`). The package has no `<depend>` on any other Custos package — it's a config-only ament package.
- Two top-level data directories exist but are empty: `airframes/`, `params/`. No real airframe template or Pixhawk parameter set has been authored yet.
- The `src/` directory under the package is empty by design — this repo does not compile code, it ships data.

## Cross-repo edges

- **Depends on:** nothing (no Custos deps, no ROS deps beyond `ament_cmake`).
- **Depended on by:** humans, not code. Hardware setup procedures reference this repo; node code does not.

## Repo-specific hard rules

- **No per-airframe identifying data** (ADR 0013, the one rule above).
- **No node implementations.** If a calibration procedure needs a runtime helper, that helper belongs in `custos-control` (Pixhawk surface) or `custos-infra` (general tooling) — not here.
- **Apache 2.0 applies to the *configuration*, not the airframe**. The license covers what's in `params/` and `airframes/`; it does not constrain how anyone flies their drone.
- **Treat parameter changes as additive.** Default parameter sets are referenced by external setup procedures; renaming a parameter set's directory or YAML key breaks every operator who pinned a specific name. Add a new set rather than mutating an old one.

## Build / test cheat sheet

```bash
# The package "builds" but emits no artifacts.
colcon build --packages-select custos_hardware_airframes
colcon test --packages-select custos_hardware_airframes

# Validate a Pixhawk parameter file before commit.
# (No tooling exists yet; will be added to custos-infra.)
```

## Pointers specific to this repo

- Public-data boundary: ADR 0013 (`custos-bringup/docs/adr/0013-public-from-day-one.md`)
- Mission/control surface that consumes these configs: `custos-control/custos_control_pixhawk/`

> TODO(post-active): write the first airframe template in `airframes/` and the first default Pixhawk parameter set in `params/`.
> TODO(post-active): add a parameter-file validator to `custos-infra/lint/` and reference it from here.
> TODO(post-active): document the private fleet/inventory system once it exists, so contributors know where serial-tagged data goes.
