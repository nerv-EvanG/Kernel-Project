# P02 // ICE DPLL

Status: Patch artifact archived locally; upstream review status is not recorded in the supplied patch.

Subsystem: Intel ICE / DPLL
Date: 2026-09-25

## What changed

Removed stale kernel-doc parameter descriptions from:

- `ice_dpll_init_fwnode_pins()`: stale `@count`
- `ice_dpll_init_pins_e825()`: stale `@cgu`

The code change is documentation-only: two parameter descriptions that no longer matched the function interfaces were removed.

## File changed

`drivers/net/ethernet/intel/ice/ice_dpll.c`

## Patch

`0001-ice-dpll-fix-kernel-doc-parameter-descriptions.patch`

## Notes

The supplied patch does not include test output, checkpatch output, or an upstream mailing-list URL. Those details should be added when the corresponding evidence is available.
