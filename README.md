# Linux Kernel Work

Upstream Linux kernel development work by Ayush Yaduvanshi.

This repository is a **development portfolio and patch archive**. It is not a fork of the Linux kernel and does not claim that archived or submitted patches were accepted upstream.

## Repository layout

```text
.
├── patches/          # Upstream patch submissions and their documentation
├── configs/          # Kernel configuration files used for local testing
└── archive/          # Historical experiments kept for provenance
```

## Upstream work

| ID | Area | Status |
|---|---|---|
| P01 | USB / sisusbvga | Submitted upstream; awaiting review |

### P01 — sisusbvga open-path deadlock

**Subject:** `USB: sisusbvga: avoid initializing device in open`

The patch removes synchronous device initialization from the USB character-device `.open()` path and treats high-speed probe-time initialization failure as a probe failure. The work was motivated by a syzbot report involving a task hang around `usb_register_dev()`.

> **Important:** submitted is not the same as accepted. Acceptance will only be recorded after the upstream kernel mailing-list process confirms it.

## Development principles

- Prefer small, reviewable upstream patches.
- Reproduce and understand the reported failure before changing code.
- Build and run relevant validation before submission.
- Follow Linux kernel coding style and commit-message conventions.
- Record upstream status separately from local experimentation.

## Links

- Linux kernel: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
- syzbot: https://syzkaller.appspot.com/

## Author

Ayush Yaduvanshi (`nerv-EvanG`)
