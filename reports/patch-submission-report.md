# Linux Kernel Patch Submission Report

**Ayush Yaduvanshi** · `nerv-EvanG`  
**Updated:** 13 November 2026  
**Focus:** Driver lifecycle, networking, CPU hotplug, performance monitoring, locking, and kernel maintenance

Most of my work has involved understanding how existing kernel code behaves, tracing issues through driver and subsystem paths, and making focused changes where the behavior or implementation needs attention. That has included initialization and teardown handling, error-path cleanup, networking-driver maintenance, locking investigations, and kernel-doc fixes. This report tracks the patches I worked on across their full lifecycle — applied changes, upstream submissions, prepared work, and investigations I decided not to send.

A patch being submitted is not the same as being accepted, so I have kept those states separate.

## Current snapshot

| State | Count | Notes |
|---|---:|---|
| Applied / accepted in a maintainer tree | **5** | Four netdev/net-next patches and one AMDGPU patch acknowledged as applied |
| Submitted; no application confirmed here | **5** | Includes patches with maintainer feedback; no merge is recorded |
| Prepared; dry-run only | **2** | AMD Power/IBS series built and dry-run checked; actual send is not confirmed here |
| Investigated, not submitted | **3 work items** | Dropped or held after technical review, conflicts, or novelty checks |

*These are contribution-tracking counts, not an official LKMP graduation decision. Programme eligibility is determined by the mentorship team.*

## Applied upstream

| Subsystem | Patch | What changed | Result |
|---|---|---|---|
| Intel ICE / DPLL | [ice: dpll: fix kernel-doc parameter descriptions](https://git.kernel.org/netdev/net-next/c/a72690652227) | Removed stale `@count` and `@cgu` descriptions that no longer matched the function interfaces. | Applied to netdev/net-next |
| Intel IDPF | [idpf: fix kernel-doc parameter descriptions](https://git.kernel.org/netdev/net-next/c/014d795c7383) | Removed stale `@vport` descriptions from two resource-release helpers. | Applied to netdev/net-next |
| Solarflare SFC | [sfc: fix kernel-doc description for efx_ptp_timeset](https://git.kernel.org/netdev/net-next/c/bbafd2f4b354) | Removed an excess `@valid` member description from `efx_ptp_timeset`. | Applied to netdev/net-next |
| Atheros ATLX | [atlx: fix kernel-doc description for atlx_tx_timeout](https://git.kernel.org/netdev/net-next/c/29b635a5bb8a) | Added the missing `@txqueue` parameter description to `atlx_tx_timeout()`. | Applied to netdev/net-next |
| AMDGPU | [drm/amdgpu: fix kernel-doc in amdgpu_gfx.h](https://lore-kernel.gnuweeb.org/amd-gfx/20261110011256.157652-1-ayush37735%40gmail.com/) | Corrected the `struct amdgpu_rb_config` kernel-doc heading, clarified member descriptions, and added an explicit `Return:` section. | Maintainer replied “Acked and applied” on 13 Nov 2026 |

## Submitted for review

| Subsystem | Patch / work | Technical focus | Current record |
|---|---|---|---|
| USB / sisusbvga | [v1 thread](https://lists.openwall.net/linux-kernel/2026/09/05/868) · [v2 thread](https://lists.openwall.net/linux-kernel/2026/09/07/738) | Moved graphics-device initialization away from the character-device `.open()` path; v2 also stops initialization after the first failed USB request and fails probe on initialization failure. | v2 was tested by syzbot and the reported hang was not reproduced. Review is still outstanding; Greg Kroah-Hartman noted the fake-device report was low priority. No merge is recorded here. |
| Solarflare Siena | [sfc: siena: fix kernel-doc description for efx_ptp_timeset](https://lists.openwall.net/linux-kernel/2026/09/29/1239) | Removed the excess `@valid` description from the Siena `efx_ptp_timeset` structure. | Received a `Reviewed-by` from Joe Damato; application is not confirmed in this report. |
| Intel ICE | [ice: Modernize ice_vsi_free() with scope-based guard(mutex)](https://lore-kernel.gnuweeb.org/intel-wired-lan/20261014110552.56976-1-ayush37735%40gmail.com/) | Replaced the explicit `mutex_lock()` / `mutex_unlock()` pair with `guard(mutex)` in `ice_vsi_free()`. | Review raised concerns about the missing commit message, clean-up-only scope, and the longer mutex critical section. An automated Sashiko review also flagged a possible TOCTOU/UAF issue, which would need investigation. No merge is recorded. |
| 8390 | [net: 8390: fix kernel-doc warning for __ei_tx_timeout](https://lists.openwall.net/linux-kernel/2026/10/26/2228) | Worked on correcting the kernel-doc description for `__ei_tx_timeout()`. | Simon Horman pointed out that the driver is orphaned and that netdev discourages standalone clean-up patches. No acceptance is recorded. |
| Broadcom bnx2x | [bnx2x: fix kernel-doc for bnx2x_rss()](https://lore-kernel.gnuweeb.org/netdev/20261109211719.114004-1-ayush37735%40gmail.com/T/) | Updated the stale function name in the kernel-doc block and removed the obsolete `@ind_table` parameter. | Submitted on 9 Nov 2026; no review or application is recorded here yet. |


## Prepared for submission

| Subsystem | Patch | Technical focus | Validation / status |
|---|---|---|---|
| AMD Power PMU | [Part 1 of the AMD perf series](https://lore.kernel.org/linux-perf-users/20261112234547.18226-2-ayush37735%40gmail.com/) | Checks `cpuhp_setup_state()` and unwinds the hotplug state if `perf_pmu_register()` fails. | `power.o` compiled; checkpatch and diff checks passed; `git send-email --dry-run` passed. Actual email delivery is not confirmed in this report. |
| AMD IBS | [Part 2 of the AMD perf series](https://lore.kernel.org/linux-perf-users/20261112234547.18226-3-ayush37735%40gmail.com/) | Checks CPU-hotplug setup, unwinds the hotplug state and syscore registration on failure, and resets `ibs_caps`. | `ibs.o` compiled; checkpatch and diff checks passed; `git send-email --dry-run` passed. Actual email delivery is not confirmed in this report. |

The AMD Power/IBS series involved AI-assisted technical discussion during revision. I am checking its eligibility with the LFX mentors separately and am not treating it as confirmed mentorship credit.

## Investigations that did not become submissions

- **YNL C generator:** I explored normalizing family names and avoiding generated enums when a family already uses UAPI-defined declarations. The generated-header build exposed enum redeclaration conflicts with UAPI headers, so I stopped rather than send a patch that did not build cleanly.
- **PCIe M.2 power sequencing:** I investigated a possible fix, but equivalent work had already been submitted upstream by the time I was ready. I did not send a duplicate.
- **r8169 guard-based cleanup:** I explored a guard-based locking change as a driver-maintenance candidate. I have no upstream submission recorded for it, so it is not included in the submission count.
- **VIMC signature patch:** The repository also keeps an early VIMC patch used during initial kernel build and patch-workflow practice. I treat it as a learning artifact, not as one of the applied contributions above.

## How I work

My usual workflow is:

```text
read the report / warning
        ↓
trace the relevant code and call paths
        ↓
identify the actual mismatch or failure path
        ↓
make the smallest reasonable change
        ↓
build the affected object / run focused checks
        ↓
checkpatch + diff checks
        ↓
format and send with git send-email
        ↓
follow review, revise, or record why I stopped
```

For the patches listed above, validation has included targeted object builds, `scripts/checkpatch.pl --strict`, `git diff --check`, kernel-doc validation, and syzbot testing where applicable. I only list a check against a patch when it was actually run.

## Notes

- “Applied” means the patch was reported as applied to the relevant maintainer/subsystem tree, or the maintainer explicitly confirmed it was applied. It does not imply that every change is already in a released stable kernel.
- “Submitted” means sent to the relevant upstream mailing list; it does not imply acceptance.
- The current record is based on mailing-list threads, application notifications, and my local patch archive. I will update it as review and merge status changes.
- The upstream mailing-list thread and maintainer tree remain the source of truth for each patch.

---

**Ayush Yaduvanshi**  
`nerv-EvanG` · Linux kernel contributor
