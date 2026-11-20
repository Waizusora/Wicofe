# Wicofe OS Architecture

**Status:** baseline proposal; subject to revision through architecture decision records (ADRs).

## 1. Design overview

Wicofe targets a configurable monolithic kernel. Core mechanisms execute in kernel space for direct interaction and predictable subsystem integration. Optional drivers and filesystem implementations may be delivered as Dynamic Kernel Modules (DKM), but the kernel retains ownership of privileged resource management and core interfaces.

The initial implementation language is Rust `no_std`; architecture-specific assembly is permitted where required for boot, CPU entry, context switching, or other low-level operations.

## 2. Layer model

### Firmware and boot

The initial boot path targets Limine and its boot protocol. Bootloader-provided information must be normalized into kernel-owned structures before the rest of the kernel depends on it. Boot protocol details must not leak throughout unrelated subsystems.

### Kernel core

The kernel is responsible for:
- CPU and architecture initialization.
- Interrupt and exception handling.
- Physical and virtual memory management.
- Scheduling, threads, processes, and synchronization.
- System call dispatch and user/kernel boundary enforcement.
- VFS and mount infrastructure.
- Device and driver lifecycle.
- Security primitives and capability/permission checks.

### Kernel modules

DKM is an optional extension mechanism, not a replacement for the monolithic kernel. The module contract must define ABI versioning, architecture, relocation/object format, symbol policy, dependency handling, initialization, teardown, and failure behavior before a stable module ecosystem is claimed.

### Userspace

Userspace contains libc and support libraries, PID 1/service supervision, package management, system daemons, command-line tools, and the desktop environment. Rust `std` is preferred when available; FFI is limited to defined OS interfaces and interoperability needs.

### Desktop

WDE is a separate userspace desktop environment. Its compositor, panel, launcher, session, and settings must communicate through documented protocols and OS interfaces rather than depending on private kernel internals.

## 3. Initial platform targets

- CPU architectures: x86-64 and AArch64.
- Boot: Limine / Limine Boot Protocol.
- Kernel: Rust `no_std`, configurable monolithic design.
- Initial filesystem direction: ONWFS and FAT32 through the VFS.
- Userspace: Rust `std` where practical.
- Original project license: MPL-2.0.

These are project decisions and targets, not claims of completed support.

## 4. Cross-component contracts

| Contract | Owning project |
|---|---|
| Syscall numbers, structures, errors, calling convention | Wicofe-ABI |
| Kernel implementation and VFS integration | Wicofe-Kernel |
| Native filesystem format and implementation | ONWFS |
| Driver core, DKM loader, and privileged DKM ABI | Wicofe-Kernel |
| Concrete optional driver implementations and driver-specific packaging | Wicofe-Driver |
| C runtime and libc integration | Wicofe-Libc |
| Shared userspace libraries | Wicofe-Lib |
| PID 1, service definitions, dependency resolution, supervision and shutdown | [Frenit](https://github.com/Waizusora/Frenit) |
| Package format and package operations | WPM |
| Whole-system release discovery, staging, activation and rollback | Wicofe-Update |
| Image manifest, system image composition and release artifacts | Wicofe-Image |
| Installation CLI/workflow and deployment orchestration | Wicofe-Installer |
| Whole-system build orchestration and artifact provenance | Wicofe-Build |
| Recovery environment, repair and restore | Wicofe-Recovery |
| Desktop session and compositor | WDE |

Frenit is Wicofe's userspace initializer and service lifecycle supervisor. Its mandatory Core Init responsibilities, optional modules, single-executable model and external-service boundary are defined in the [Frenit project overview](https://github.com/Waizusora/Frenit/blob/main/README.md). The owning repository maintains implementation details; this documentation repository records system-wide decisions and links to canonical specifications.

The userspace syscall ABI is owned by [Wicofe-ABI](https://github.com/Waizusora/Wicofe-ABI). The separate privileged DKM ABI is owned by [Wicofe-Kernel](https://github.com/Waizusora/Wicofe-Kernel); it must not be treated as the userspace syscall ABI. See the kernel repository's [ABI boundary specification](https://github.com/Waizusora/Wicofe-Kernel/blob/main/docs/ABI_BOUNDARIES.md).

## 5. Memory management direction

The current kernel design direction is a staged hybrid:
1. Early boot allocator for initialization.
2. Physical memory manager using buddy allocation, with bitmap or equivalent metadata as appropriate.
3. Virtual memory manager for address spaces and mappings.
4. Kernel heap using size-class/slab-style allocation backed by physical pages.

Exact algorithms, metadata placement, NUMA strategy, reclaim behavior, and page-size policy remain kernel-level design decisions. See the kernel repository's memory-management specification.

## 6. Filesystem direction

VFS is part of the kernel, not a separate repository. ONWFS is the planned native filesystem. FAT32 is an initial interoperability target. Other filesystem implementations may be optional modules when the module and boot dependencies permit it.

The on-disk format, crash-consistency model, journaling or copy-on-write strategy, checksumming, recovery, and compatibility policy must be specified before ONWFS is treated as stable.

## 7. Security boundaries

- Treat userspace pointers and all external input as untrusted.
- Validate lengths, offsets, identifiers, and state transitions at subsystem boundaries.
- Define ownership and lifetime rules for kernel objects.
- Do not load modules or packages without an explicit trust and integrity policy.
- Keep privilege transitions auditable.
- Document threat models for boot, updates, storage, networking, and module loading.

## 8. Status vocabulary

Use these labels consistently:
- **Implemented:** code exists.
- **Tested:** automated or documented validation has passed.
- **Experimental:** code exists but interfaces or behavior may change.
- **Planned:** accepted direction, not implemented.
- **Deferred:** intentionally postponed.
- **Rejected:** considered and not selected.

A design document alone does not establish implementation status.
