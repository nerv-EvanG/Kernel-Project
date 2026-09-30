# P03 // IDPF

Status: Patch artifact archived locally; upstream review status is not recorded in the supplied patch.

Subsystem: Intel IDPF
Date: 2026-09-25

## What changed

Removed stale kernel-doc parameter descriptions from:

- `idpf_rx_desc_rel_all()`: stale `@vport`
- `idpf_vport_queue_grp_rel_all()`: stale `@vport`

The change keeps the documentation aligned with the functions' actual parameter lists.

## File changed

`drivers/net/ethernet/intel/idpf/idpf_txrx.c`

## Patch

`0001-idpf-fix-kernel-doc-parameter-descriptions.patch`

## Notes

The supplied patch does not include test output, checkpatch output, or an upstream mailing-list URL. Those details should be added when the corresponding evidence is available.
