# P06 // ATLX

Status: Patch artifact archived locally; upstream review status is not recorded in the supplied patch.

Subsystem: Atheros ATLX
Date: 2026-09-29

## What changed

Added the missing `@txqueue` kernel-doc parameter description to `atlx_tx_timeout()`:

`@txqueue: transmit queue index`

The patch was intended to eliminate the kernel-doc warning caused by the undocumented function parameter.

## File changed

`drivers/net/ethernet/atheros/atlx/atlx.c`

## Patch

`0001-atlx-fix-kernel-doc-description-for-atlx_tx_timeout.patch`

## Notes

The supplied patch does not include test output, checkpatch output, or an upstream mailing-list URL. Those details should be added when the corresponding evidence is available.
