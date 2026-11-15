# ADR 0001: Wicofe Project Baseline

- **Status:** Accepted
- **Date:** 2026-11-16

## Context

Wicofe is developed across multiple repositories. Without shared constraints, kernel, ABI, filesystem, service, and desktop implementations could drift or make incompatible assumptions.

## Decision

1. Wicofe targets an independent Unix-like operating system.
2. The kernel is configurable monolithic and primarily Rust `no_std`.
3. Initial CPU targets are x86-64 and AArch64.
4. Limine is the initial bootloader/protocol direction.
5. VFS is owned by Wicofe-Kernel; ONWFS is the planned native filesystem.
6. DKM is an optional extension mechanism and requires a separately versioned contract.
7. Userspace prefers Rust `std` where practical; FFI is used at explicit interoperability boundaries.
8. Original project code targets MPL-2.0, subject to repository-specific notices and third-party license review.
9. Wicofe is the system-wide documentation and architecture coordination repository.

## Consequences

- Wicofe-ABI is the canonical location for syscall and userspace ABI definitions.
- Component repositories own implementation-specific documentation.
- Cross-repository interfaces require explicit versioning and compatibility policy.
- These decisions do not imply that the described features are implemented.
