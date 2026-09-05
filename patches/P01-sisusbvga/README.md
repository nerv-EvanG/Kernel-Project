# `P01 // SISUSBVGA`

```text
STATUS       : SUBMITTED / REVIEW
SUBSYSTEM     : USB
REPORT        : syzbot / task hung in usb_register_dev
PATCH        : USB: sisusbvga: avoid initializing device in open
```

## `trace`

syzbot reported a task hang involving the USB character-device registration path. The USB core holds `minor_rwsem` while invoking a USB character device's `.open()` callback. `sisusb_open()` could then take `sisusb->lock` and perform synchronous USB device initialization.

That makes the open path perform potentially blocking device initialization while the USB core's minor semaphore is held.

## `change`

The patch removes lazy graphics-device initialization from `sisusb_open()`.

High-speed devices are initialized during probe instead. If that probe-time initialization fails, probing is failed rather than leaving the device to retry initialization later from the character-device open path.

The goal is a narrower open path: validate the device, acquire the reference, and open it — without performing synchronous initialization there.

## `validation`

```text
[ OK ] full kernel build
[ OK ] git diff --check
[ OK ] checkpatch.pl --strict — 0 errors
[ 1  ] checkpatch warning — no speculative Fixes: tag
```

No introducing commit was identified for a defensible `Fixes:` tag, so none was invented.

## `upstream`

**Commit:** `be50fa1b2def095afcaec4ca9eb885d99d8f0f6b`  
**Subject:** `[PATCH v1] USB: sisusbvga: avoid initializing device in open`  
**Author:** Ayush <grimstonbusiness@gmail.com>  
**Status:** Submitted upstream; awaiting review.

The upstream mailing-list thread remains authoritative for review and acceptance status. This repository is a portfolio/archive copy, not the canonical upstream source.

---

```text
next → review → revision → acceptance
```
