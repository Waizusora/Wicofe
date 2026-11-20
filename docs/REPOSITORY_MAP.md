# Wicofe Repository Map

This document defines the intended responsibility of each Wicofe repository. It is a project map, not a statement that all repositories already contain working implementations. For per-repository documentation ownership and canonical technical indexes, see the [Wicofe-Doc repository documentation map](https://github.com/Waizusora/Wicofe-Doc/blob/main/REPOSITORY_DOCUMENTATION_MAP.md).

## Core and interfaces

| Repository | Responsibility |
|---|---|
| [Wicofe-Kernel](https://github.com/Waizusora/Wicofe-Kernel) | Monolithic Rust kernel, architecture support, memory, scheduler, syscall implementation, VFS, module framework |
| [Wicofe-ABI](https://github.com/Waizusora/Wicofe-ABI) | Draft public kernel/userspace ABI baseline, syscall contract, and shared interface definitions; not yet declared stable |
| [WLibc](https://github.com/Waizusora/WLibc) | C standard library and POSIX runtime adapted to the native Wicofe ABI; GNU/BSD compatibility extensions are out of scope |
| [Wicofe-Lib](https://github.com/Waizusora/Wicofe-Lib) | Shared Wicofe userspace libraries and Rust-facing support APIs |
| [ONWFS](https://github.com/Waizusora/ONWFS) | Native filesystem format, implementation, tooling, and compatibility tests |

## System services and platform

| Repository | Responsibility |
|---|---|
| [Frenit](https://github.com/Waizusora/Frenit) | Free Init; init-system and service-management implementation for Wicofe |
| [WPM](https://github.com/Waizusora/WPM) | Package manager, package metadata/format, repositories, dependency and transaction model |
| [Wicofe-Storage](https://github.com/Waizusora/Wicofe-Storage) | Userspace storage discovery, partitioning, formatting, mount and volume tools; kernel storage interfaces remain in Kernel |
| [Wicofe-Driver](https://github.com/Waizusora/Wicofe-Driver) | Driver source/packaging and DKM integration guidance; core driver framework remains in Kernel |
| [Wicofe-Service](https://github.com/Waizusora/Wicofe-Service) | Userspace daemons such as device, logging, user/session, power, and system service components |
| [Wicofe-Network](https://github.com/Waizusora/Wicofe-Network) | Network userspace services, configuration, diagnostics, and protocol utilities |
| [Wicofe-Input](https://github.com/Waizusora/Wicofe-Input) | Input stack userspace integration, device policy, configuration, and utilities |
| [Wicofe-Graphic](https://github.com/Waizusora/Wicofe-Graphic) | Graphics userspace stack, display integration, rendering support, and related tools |
| [Wicofe-Audio](https://github.com/Waizusora/Wicofe-Audio) | Audio services, routing, device policy, and userspace audio APIs |

## User experience and lifecycle

| Repository | Responsibility |
|---|---|
| [WDE](https://github.com/Waizusora/WDE) | Wayland desktop environment, compositor, panel, launcher, session, settings |
| [Mysh](https://github.com/Waizusora/Mysh) | Independent command-line shell; Wicofe integration is a planned shell target. Package management belongs to WPM, not Mysh |
| [Wicofe-Installer](https://github.com/Waizusora/Wicofe-Installer) | Installation workflow, disk layout, deployment, and first-boot setup |
| [Wicofe-Update](https://github.com/Waizusora/Wicofe-Update) | Update metadata, verification, staging, rollback, and system update client |
| [Wicofe-Recovery](https://github.com/Waizusora/Wicofe-Recovery) | Recovery environment, repair workflows, diagnostics, and restore |
| [Wicofe-Image](https://github.com/Waizusora/Wicofe-Image) | OS image composition, manifests, reproducible image assembly |

## Engineering infrastructure

| Repository | Responsibility |
|---|---|
| [Wicofe-Build](https://github.com/Waizusora/Wicofe-Build) | Build orchestration, toolchain pinning, cross-compilation, image pipeline |
| [Wicofe-SDK](https://github.com/Waizusora/Wicofe-SDK) | Developer SDK, target definitions, headers, templates, sysroot and tooling integration |
| [Wicofe-Port](https://github.com/Waizusora/Wicofe-Port) | Port recipes, patches, build metadata, and upstream tracking |

## Project-wide engineering repositories

| Repository | Responsibility |
|---|---|
| [Wicofe-Tool](https://github.com/Waizusora/Wicofe-Tool) | Shared development tooling, repository validation, release helpers, and audit utilities |
| [Wicofe-Doc](https://github.com/Waizusora/Wicofe-Doc) | User, administrator, developer, and contributor documentation |
| [Wicofe-Spec](https://github.com/Waizusora/Wicofe-Spec) | Normative cross-component specifications and compatibility contracts |
| [Wicofe-Test](https://github.com/Waizusora/Wicofe-Test) | Cross-repository integration, conformance, regression, and system tests |
| [Wicofe-ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty) | Third-party inventory, provenance, license records, and patch tracking |

These repositories now exist. Their initial README files define scope and ownership; implementation, policy adoption, and CI coverage are separate milestones.

## Boundary rules

1. Kernel mechanisms and VFS implementation belong in Wicofe-Kernel.
2. ABI definitions belong in Wicofe-ABI; kernel and userspace implementations must not independently redefine them.
3. ONWFS owns its disk-format specification and filesystem-specific tests; Kernel owns VFS integration.
4. Wicofe-Driver does not duplicate the kernel's driver core.
5. Frenit owns its init-system and service-management implementation; individual daemons belong to Wicofe-Service or their subsystem.
6. WDE is a userspace desktop and must not require private kernel APIs.
7. Cross-repository integration tests should eventually be centralized in Wicofe-Test.
