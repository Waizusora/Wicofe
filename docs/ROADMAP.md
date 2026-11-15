# Wicofe OS Roadmap

The roadmap is dependency-driven. A milestone is complete only when its exit criteria are met and recorded; repository creation alone does not count as implementation.

## Phase 0 — Project baseline

- [x] Establish repository responsibilities.
- [x] Record system architecture direction.
- [ ] Add consistent contribution, security, and licensing policies to all repositories.
- [ ] Establish architecture decision record (ADR) process.
- [ ] Define project-wide status and versioning conventions.

**Exit:** system boundaries and project policies are documented and internally consistent.

## Phase 1 — Kernel and ABI foundation

- [ ] Freeze an initial syscall ABI draft.
- [ ] Define boot handoff and kernel entry contracts.
- [ ] Implement architecture bring-up for x86-64.
- [ ] Establish exception and interrupt handling.
- [ ] Implement early physical memory discovery and allocator.
- [ ] Define scheduler and process/thread model.
- [ ] Establish serial/console diagnostics and panic behavior.

**Exit:** kernel reaches a controlled diagnostic state under the selected emulator on the first target architecture.

## Phase 2 — Memory, tasks, and userspace entry

- [ ] Implement PMM and VMM.
- [ ] Implement kernel heap and synchronization primitives.
- [ ] Implement task scheduling and user address spaces.
- [ ] Implement syscall dispatch and user/kernel copy validation.
- [ ] Define executable loading and initial process startup.

**Exit:** a minimal userspace program can start and use a documented syscall subset.

## Phase 3 — Storage and filesystems

- [ ] Define block-device interface.
- [ ] Define VFS object and mount model.
- [ ] Implement initial FAT32 read support.
- [ ] Specify ONWFS on-disk format and recovery behavior.
- [ ] Implement ONWFS after format review and test vectors.
- [ ] Add filesystem conformance and corruption tests.

**Exit:** filesystems can be mounted and exercised through the common VFS with repeatable tests.

## Phase 4 — Drivers and system initialization

- [ ] Define driver lifecycle and device model.
- [ ] Define DKM ABI, object format, relocation and trust policy.
- [ ] Implement essential console, storage, timer, and input drivers.
- [ ] Implement Osynit as PID 1.
- [ ] Define service dependency and supervision semantics.

**Exit:** the system boots into a minimal managed userspace and can shut down cleanly.

## Phase 5 — Usable base system

- [ ] Complete libc and core userspace library integration.
- [ ] Establish package format and WPM transaction model.
- [ ] Add network and system service foundations.
- [ ] Integrate Mysh and essential system tools.
- [ ] Produce reproducible system images.

**Exit:** a minimal installable command-line system can be updated and diagnosed.

## Phase 6 — Graphics and desktop

- [ ] Establish display and graphics userspace interfaces.
- [ ] Implement input integration and session management.
- [ ] Bring up WDE compositor and nested development backend.
- [ ] Implement panel, launcher, settings, and login/session flow.
- [ ] Validate accessibility, stability, and resource use.

**Exit:** a usable graphical session runs on supported hardware or emulator targets.

## Phase 7 — Reliability and release engineering

- [ ] Implement installer, updater, and recovery workflows.
- [ ] Add cross-repository integration and conformance suites.
- [ ] Establish security response and vulnerability disclosure process.
- [ ] Audit all shipped dependencies and license obligations.
- [ ] Define release, support, and compatibility policies.

**Exit:** release candidates pass documented boot, install, update, recovery, and regression tests.

## Parallel development rule

Userspace repositories may develop prototypes against mocks or host platforms, but must not claim native Wicofe compatibility until the corresponding ABI and kernel services exist. Cross-repository interfaces should be versioned and reviewed before dependent implementations are treated as stable.
