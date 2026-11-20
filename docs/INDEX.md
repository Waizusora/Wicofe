# Wicofe Project Documentation Index

This repository documents the whole Wicofe operating system at project level. It does not replace component-owned implementation documentation or normative cross-component specifications.

## Project-level documents

- [System architecture](ARCHITECTURE.md)
- [Roadmap](ROADMAP.md)
- [System delivery and installation direction 0.1](https://github.com/Waizusora/Wicofe-Doc/blob/main/SYSTEM_DELIVERY_AND_INSTALLATION_DIRECTION_0.1.md) — planned CLI installation, WPM update entry point and Delivery Release model; not implementation evidence.
- [Repository map](REPOSITORY_MAP.md)
- [Architecture decision records](../decisions/README.md)
- [Frenit repository and CLI](https://github.com/Waizusora/Frenit/blob/main/README.md)
- [Frenit integration contract 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/boot/FRENIT_INTEGRATION_CONTRACT_0.1.md)
- [Contributing](../CONTRIBUTING.md)
- [Security policy](../SECURITY.md)

## Documentation authorities

- [Central documentation index](https://github.com/Waizusora/Wicofe-Doc/blob/main/INDEX.md)
- [Repository documentation map](https://github.com/Waizusora/Wicofe-Doc/blob/main/REPOSITORY_DOCUMENTATION_MAP.md)
- [Cross-component specifications](https://github.com/Waizusora/Wicofe-Spec)

## Historical material

- [Archived full OS blueprint 0.1](archive/FULL_OS_BLUEPRINT_0.1.md) — retained for history only; superseded by the current architecture, roadmap, and repository map.

## Boundary

This repository owns whole-system architecture, project direction, repository relationships, and project-level decisions. Kernel internals belong in Wicofe-Kernel; public syscall ABI in Wicofe-ABI; ONWFS disk format in ONWFS; and shared contracts in Wicofe-Spec. User, administrator, and developer guides belong in Wicofe-Doc.
