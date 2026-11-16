# Wicofe OS

Wicofe is an independent Unix-like operating system project built around a Rust-based monolithic kernel and a modular userspace.

> **Project status:** early architecture and foundation phase. Repository descriptions and roadmaps distinguish implemented code from proposals; the project does not claim to be bootable or production-ready.

## Project direction

- Monolithic kernel primarily written in Rust `no_std`.
- x86-64 and AArch64 as initial architecture targets.
- Dynamic Kernel Modules (DKM) for optional kernel components, subject to a versioned and documented module ABI.
- A kernel-owned VFS with ONWFS as the planned native filesystem.
- Unix-like userspace interfaces, with POSIX compatibility as a long-term objective.
- Rust `std` for userspace where practical; FFI only at necessary OS or library boundaries.
- MPL-2.0 for original Wicofe components, with dependency-by-dependency license and provenance review.

## System at a glance

```text
Firmware
  └─ Limine boot flow
      └─ Wicofe monolithic kernel
          ├─ Architecture / CPU / interrupt layer
          ├─ Memory management
          ├─ Scheduler and process model
          ├─ VFS ── ONWFS / FAT32 / future filesystems
          ├─ Driver framework and DKM
          └─ Syscall interface (Wicofe ABI)
              └─ Userspace
                  ├─ Wicofe-Libc / Wicofe-Lib
                  ├─ Osynit (PID 1 and service supervision)
                  ├─ WPM (package manager)
                  └─ WDE (desktop environment)
```

This is a target architecture, not a statement that every component is implemented.

## Repositories

See [Project documentation index](docs/INDEX.md) and [Repository map](docs/REPOSITORY_MAP.md) for whole-system architecture, repository ownership, and cross-project responsibilities.

The [central documentation map](https://github.com/Waizusora/Wicofe-Docs/blob/main/REPOSITORY_DOCUMENTATION_MAP.md) links each component to its own technical documentation.\n\nProject-wide engineering repositories: [Tools](https://github.com/Waizusora/Wicofe-Tools) · [Docs](https://github.com/Waizusora/Wicofe-Docs) · [Specs](https://github.com/Waizusora/Wicofe-Specs) · [Tests](https://github.com/Waizusora/Wicofe-Tests) · [ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty).

## Architecture and planning

- [System architecture](docs/ARCHITECTURE.md)
- [Roadmap](docs/ROADMAP.md)
- [Architecture decision records](decisions/README.md)
- [Contributing](CONTRIBUTING.md)
- [Security policy](SECURITY.md)
- [Project governance](https://github.com/Waizusora/Wicofe-Docs/blob/main/GOVERNANCE.md)
- [License and third-party policy](https://github.com/Waizusora/Wicofe-Docs/blob/main/LICENSE_POLICY.md)

## Project principles

1. **Explicit contracts:** kernel/userspace, module, filesystem, and service interfaces must be documented.
2. **Small core:** keep the kernel and base userspace focused; optional functionality should remain modular where practical.
3. **Security by design:** validate untrusted inputs, define privilege boundaries, and avoid implicit trust in modules or packages.
4. **License discipline:** audit direct and transitive dependencies, optional features, generated code, and copied material.
5. **Honest status:** distinguish implemented, tested, experimental, planned, and deferred work.

## Licensing

Original Wicofe code is intended to use the Mozilla Public License 2.0 (MPL-2.0), unless a repository explicitly documents an approved exception. Third-party components retain their own licenses. See each repository's license and dependency notices before reuse.
