# Security Policy

## Scope

This policy covers security vulnerabilities in Wicofe source code, build tooling, release artifacts, specifications, and supported project infrastructure.

Wicofe is an early-stage project. A component must not be considered security-audited or production-ready unless that status is explicitly documented with supporting evidence.

## Reporting a Vulnerability

Do not disclose suspected vulnerabilities in public issues, discussions, or pull requests.

Use GitHub's **Report a vulnerability** / private vulnerability reporting feature for this repository when available. Include:

- Affected repository, component, revision, and version.
- Impact and realistic attack scenario.
- Reproduction steps or a minimal proof of concept.
- Relevant logs, traces, or crash information.
- Any suggested mitigation, if known.

If private reporting is unavailable, contact the repository owner through the contact method listed on the GitHub profile and request a private security-reporting channel. Do not send exploit details through a public issue.

## Response and Disclosure

The maintainers will assess scope, severity, reproducibility, affected versions, and mitigation options. Do not assume a fixed response or remediation deadline.

Coordinate public disclosure with maintainers. Avoid publishing exploit details while users remain exposed and no coordinated disclosure plan exists.

## Third-Party Components

Vulnerabilities in upstream dependencies should be reported to the upstream maintainers as appropriate and recorded in Wicofe's third-party component inventory when they affect Wicofe.

## Security Claims

Passing CI, compiling successfully, or booting in an emulator is not a security audit. Security claims must identify the exact component, revision, test method, and limitations.
