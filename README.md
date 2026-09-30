# Linux Kernel Work

Upstream Linux kernel development work by Ayush Yaduvanshi.

This repository is a **development portfolio and patch archive**. It is not a fork of the Linux kernel and does not claim that archived or submitted patches were accepted upstream.

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

## Contribution themes

The current archive covers:

- Linux kernel documentation correctness and kernel-doc hygiene.
- Networking driver maintenance across Intel, Atheros, and Solarflare code.
- USB character-device open-path behavior and syzbot-reported locking/blocking concerns.
- Building, patching, checking, and preparing Linux kernel changes for upstream contribution.

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
