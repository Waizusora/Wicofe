# ADR 0002: Frenit Init-System Direction

- **Status:** Accepted project naming and repository ownership; runtime architecture remains proposed
- **Date:** 2026-11-18
- **Canonical project:** [Frenit](https://github.com/Waizusora/Frenit)
- **Cross-component contract:** [Frenit Integration Contract 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/boot/FRENIT_INTEGRATION_CONTRACT_0.1.md)

## Context

Wicofe requires a native userspace init system. The canonical implementation repository is Frenit. Earlier init-system proposals, code, specifications, command names, and architecture decisions are not adopted or treated as compatibility requirements.

## Decision

1. The project name is **Frenit**, expanded as **Free Init**.
2. The canonical repository is `Waizusora/Frenit`.
3. The executable, Cargo package, library crate, and command prefix are `frenit`.
4. The CLI command shape is `frenit <domain> <action> [argument]`; help and version entry points are `frenit help [domain]` and `frenit --version`.
5. The CLI naming conventions are `diagnostic`, `dependent`, and `command` (singular).
6. The Frenit repository is authoritative for its implementation. Wicofe-Kernel owns kernel mechanisms; Wicofe-ABI owns public syscall contracts; Wicofe-Spec owns cross-component requirements; Wicofe-Test owns integration/conformance tests.
7. PID 1 startup, process lifecycle, signal/wait semantics, service IPC, shutdown, and boot-image handoff remain integration prerequisites. No unsupported kernel syscall or runtime capability may be assumed.
8. The current Frenit README explicitly identifies the code as an early foundation and not yet safe to install as PID 1. Wicofe must preserve that status until native conformance evidence exists.

## Consequences

- Wicofe documentation and repository maps refer to Frenit as the init-system project.
- Existing proposal-specific architecture and boot/service contracts are withdrawn from the Wicofe specification index and are not copied into Frenit.
- Kernel/ABI integration is staged only after the relevant primitives are specified and implemented.
- Build, image, and installer repositories must consume the Frenit artifact only after its target ABI and packaging contract are validated.

## References

- [Frenit README and CLI convention](https://github.com/Waizusora/Frenit/blob/main/README.md)
- [Frenit Integration Contract 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/boot/FRENIT_INTEGRATION_CONTRACT_0.1.md)
