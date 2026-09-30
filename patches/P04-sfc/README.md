# P04 // SFC

Status: Patch artifact archived locally; upstream review status is not recorded in the supplied patch.

Subsystem: Solarflare / SFC
Date: 2026-09-29

## What changed

Removed the excess `@valid` struct member description from `efx_ptp_timeset`.

The patch keeps the kernel-doc block consistent with the documented members of the structure.

## File changed

`drivers/net/ethernet/sfc/ptp.c`

## Patch

`0001-sfc-fix-kernel-doc-description-for-efx_ptp_timeset.patch`

## Notes

The supplied patch does not include test output, checkpatch output, or an upstream mailing-list URL. Those details should be added when the corresponding evidence is available.
