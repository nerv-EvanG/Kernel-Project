# P05 // SFC Siena

Status: Patch artifact archived locally; upstream review status is not recorded in the supplied patch.

Subsystem: Solarflare Siena / SFC
Date: 2026-09-29

## What changed

Removed the excess `@valid` struct member description from `efx_ptp_timeset`.

This is the Siena counterpart of the SFC P04 documentation fix.

## File changed

`drivers/net/ethernet/sfc/siena/ptp.c`

## Patch

`0001-sfc-siena-fix-kernel-doc-description-for-efx_ptp_tim.patch`

## Notes

The supplied patch does not include test output, checkpatch output, or an upstream mailing-list URL. Those details should be added when the corresponding evidence is available.
