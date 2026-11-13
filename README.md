# Linux Kernel Work

Upstream Linux kernel development work by Ayush Yaduvanshi.

This repository is a **development portfolio and patch archive**. It is not a fork of the Linux kernel and does not claim that archived or submitted patches were accepted upstream.

## Patch submission report

For the full contribution log — applied patches, upstream submissions and review feedback, prepared patch series, and investigations that I chose not to submit — see the [Linux Kernel Patch Submission Report](reports/patch-submission-report.md).

## Portfolio

| ID | Area | Focus | Date |
|---|---|---|---|
| P01 | USB / sisusbvga | Avoid device initialization in the character-device `.open()` path | 2026-09-06 |
| P02 | Intel ICE / DPLL | Remove stale kernel-doc parameter descriptions | 2026-09-25 |
| P03 | Intel IDPF | Remove stale kernel-doc parameter descriptions | 2026-09-25 |
| P04 | SFC | Remove excess `@valid` kernel-doc member description | 2026-09-29 |
| P05 | SFC Siena | Remove excess `@valid` kernel-doc member description | 2026-09-29 |
| P06 | ATLX | Add missing `@txqueue` kernel-doc parameter description | 2026-09-29 |


## Repository layout

```text
.
├── patches/
│   ├── P01-sisusbvga/
│   ├── P02-ice-dpll/
│   ├── P03-idpf/
│   ├── P04-sfc/
│   ├── P05-sfc-siena/
│   └── P06-atlx/
├── configs/          # Kernel configuration files used for local testing
└── 0001-media-vimc-add-Ayush-s-first-kernel-signature.patch
```

The VIMC patch at the repository root is the original foundational test patch used to verify kernel build/module-loading work.

## Engineering work

My kernel work is broader than documentation fixes. It includes tracing driver behavior, following initialization and teardown paths, checking error handling, and preparing focused changes for upstream review.

- **Driver lifecycle and failure handling:** USB device initialization, CPU-hotplug registration, PMU/IBS setup, and cleanup when initialization or registration fails.
- **Networking drivers:** Maintenance and review across Intel ICE/IDPF, Broadcom bnx2x, Atheros ATLX, Solarflare SFC/Siena, and the 8390 subsystem.
- **Locking and resource management:** Investigation of mutex-guard conversions, resource-release paths, and driver cleanup behavior.
- **Kernel interfaces and documentation:** Kernel-doc consistency fixes where declarations, parameters, or structure members no longer matched their documentation.
- **Kernel development workflow:** Building affected objects, checking diffs and patch style, preparing patch series, and tracking upstream review.

The [patch submission report](reports/patch-submission-report.md) records the individual changes, their technical scope, and their current upstream status.

## Upstream status

This portfolio deliberately separates **local archival state** from **upstream acceptance**.

A patch being present here means the patch artifact is preserved. It does **not** by itself mean the patch was accepted into mainline Linux. Upstream review state should be updated from the authoritative kernel mailing-list thread or merged kernel history.

## Development workflow

The work in this repository is associated with the normal kernel contribution workflow:

```text
reproduce / understand
        ↓
make a focused change
        ↓
build + validate
        ↓
checkpatch / diff checks
        ↓
git format-patch
        ↓
git send-email
        ↓
upstream review
        ↓
revision / acceptance
```

## Foundational build work

Earlier local kernel-development work included building a custom Linux kernel, using an `EXTRAVERSION` suffix for a recognizable local build, creating patches, running `scripts/checkpatch.pl`, using `git format-patch`, and preparing submissions with `git send-email`.

Those build and workflow details are kept here as development context; only patch artifacts actually present in the repository are treated as contribution records.

## Links

- Linux kernel: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
- syzbot: https://syzkaller.appspot.com/

## Author

Ayush Yaduvanshi (`nerv-EvanG`)
