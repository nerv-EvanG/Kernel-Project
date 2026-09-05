# P01 — USB sisusbvga open-path deadlock

**Status:** Submitted upstream — awaiting review  
**Subsystem:** USB / sisusbvga  
**Syzkaller report:** `INFO: task hung in usb_register_dev (3)`  
**Patch:** `USB: sisusbvga: avoid initializing device in open`

## Problem

syzbot reported a task hang involving the USB character-device registration path. The USB core holds `minor_rwsem` while invoking a USB character device's `.open()` callback. `sisusb_open()` could then take `sisusb->lock` and perform synchronous USB device initialization.

That makes the open path perform potentially blocking device initialization while the USB core's minor semaphore is held.

## Change

The patch removes lazy graphics-device initialization from `sisusb_open()`.

High-speed devices are initialized during probe instead. If that probe-time initialization fails, probing is failed rather than leaving the device to retry initialization later from the character-device open path.

This keeps the open callback focused on validating and opening an already initialized device and avoids synchronous device initialization from that path.

## Validation

- Full kernel build completed successfully.
- `git diff --check` passed.
- `checkpatch.pl --strict`: 0 errors; 1 warning concerning the absence of a `Fixes:` tag. No introducing commit was identified, so no speculative `Fixes:` tag was added.

## Upstream submission

**Commit:** `be50fa1b2def095afcaec4ca9eb885d99d8f0f6b`  
**Subject:** `[PATCH v1] USB: sisusbvga: avoid initializing device in open`  
**Author:** Ayush <ayush37735@gmail.com>  
**Reported-by:** syzbot  
**Status:** Submitted to the Linux USB mailing list and driver maintainers; not yet accepted.

The upstream mailing-list thread is the authoritative source for review status. This repository mirrors the work for portfolio/documentation purposes only.
