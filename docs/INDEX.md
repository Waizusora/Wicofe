# Wicofe Project Documentation Index

This repository documents the whole Wicofe operating system at project level. It does not replace component-owned implementation documentation or normative cross-component specifications.

## Project-level documents

- [System architecture](ARCHITECTURE.md)
- [Roadmap](ROADMAP.md)
- [Repository map](REPOSITORY_MAP.md)
- [Architecture decision records](../decisions/README.md)
- [OSynit system specification 0.1](https://github.com/Waizusora/Osynit/blob/main/docs/OSYNIT_SYSTEM_SPEC_0.1.md)
- [Contributing](../CONTRIBUTING.md)
- [Security policy](../SECURITY.md)

## Documentation authorities

- [Central documentation index](https://github.com/Waizusora/Wicofe-Docs/blob/main/INDEX.md)
- [Repository documentation map](https://github.com/Waizusora/Wicofe-Docs/blob/main/REPOSITORY_DOCUMENTATION_MAP.md)
- [Cross-component specifications](https://github.com/Waizusora/Wicofe-Specs)

## Historical material

- [Archived full OS blueprint 0.1](archive/FULL_OS_BLUEPRINT_0.1.md) — retained for history only; superseded by the current architecture, roadmap, and repository map.

## Boundary

This repository owns whole-system architecture, project direction, repository relationships, and project-level decisions. Kernel internals belong in Wicofe-Kernel; public syscall ABI in Wicofe-ABI; ONWFS disk format in ONWFS; and shared contracts in Wicofe-Specs. User, administrator, and developer guides belong in Wicofe-Docs.
