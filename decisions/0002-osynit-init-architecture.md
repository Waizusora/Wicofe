# ADR 0002: OSynit Init and Service Lifecycle Architecture

- **Status:** Accepted
- **Date:** 2026-11-16
- **Canonical project:** [OSynit](https://github.com/Waizusora/Osynit)
- **Cross-component contract:** [OSynit Core Architecture Contract 0.1](https://github.com/Waizusora/Wicofe-Specs/blob/main/boot/OSYNIT_CORE_ARCHITECTURE_CONTRACT_0.1.md)

## Context

Wicofe needs a native userspace initializer and service lifecycle supervisor. Its responsibilities must be separated from kernel mechanisms and from the domain logic of individual system daemons. The project also needs a stable identity, executable name, command namespace, and cross-repository ownership boundary.

## Decision

1. The project name is **OSynit**, expanded as **Open System Initialize**.
2. The only official executable and command prefix is `osynit`.
3. The same executable has two modes: init mode when launched as PID 1, and explicit client mode for subcommands outside PID 1. Client mode never starts another manager.
4. Core Init has twelve mandatory logical responsibilities: Kernel Interface, Process Supervisor, Service Manager, Dependency Manager, Boot Manager, System State Manager, Signal Manager, Shutdown Manager, Configuration Loader, Runtime Manager, Failure Recovery Manager, and IPC / Control Interface.
5. Mount, socket activation, timer activation, logging backends, resource/cgroup integration, security sandboxing, watchdog integration, and advanced job control are optional modules. Their absence must not prevent Core Init from operating.
6. Network, device, storage, user/session, time, audio, graphics, desktop, and container domain behavior belongs to external services or narrower subsystem repositories. OSynit supervises their lifecycle but does not embed their domain logic in PID 1.
7. The initial local manager endpoint is `/run/osynit/osynit.sock`. The protocol must be versioned, framed, bounded, permission-checked, and authorized per operation.
8. Kernel mechanisms and public userspace ABI remain owned by Wicofe-Kernel and Wicofe-ABI. OSynit must not invent syscall numbers or assume Linux-only facilities.
9. The complete command namespace is documented as a planned interface. A listed command is not considered implemented until code and tests demonstrate it.

## Consequences

- OSynit remains a small, auditable Rust userspace component with platform-specific operations isolated behind an interface.
- Wicofe-Specs coordinates shared boot and service contracts.
- Wicofe-Build, Wicofe-Image, and Wicofe-Installer integrate the binary and configuration through versioned artifact/boot contracts.
- Wicofe-Services and narrower repositories own daemon domain behavior.
- Implementation and verification status must be tracked separately for every target architecture.
- This ADR accepts the architecture boundary; it does not claim native PID 1, IPC, complete CLI, or bootable image support.

## Alternatives considered

- **Embed every manager in PID 1:** rejected because it expands the privileged core and couples unrelated domain behavior to the init process.
- **Create separate init and control executables:** rejected in favor of one executable with defensive PID 1/client dispatch.
- **Require all optional managers at boot:** rejected because optional facilities must not become prerequisites for Core Init.
- **Implement network/device/storage managers inside OSynit:** rejected; these remain external services.

## References

- [OSynit System Specification 0.1](https://github.com/Waizusora/Osynit/blob/main/docs/OSYNIT_SYSTEM_SPEC_0.1.md)
- [OSynit CLI Reference 0.1](https://github.com/Waizusora/Osynit/blob/main/docs/CLI_REFERENCE_0.1.md)
- [OSynit Core Architecture Contract 0.1](https://github.com/Waizusora/Wicofe-Specs/blob/main/boot/OSYNIT_CORE_ARCHITECTURE_CONTRACT_0.1.md)
