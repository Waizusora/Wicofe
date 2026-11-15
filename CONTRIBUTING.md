# Contributing to Wicofe

## Before contributing

- Read the repository map and the relevant component documentation.
- Check existing issues and pull requests to avoid duplicate work.
- Identify the owning repository for the change.
- For cross-component changes, describe the affected interfaces and migration plan.

## Engineering expectations

- Keep changes focused and reviewable.
- Document public interfaces, invariants, error behavior, and security assumptions.
- Add tests for behavior and regression fixes.
- Do not claim support for an architecture, feature, or compatibility level without reproducible validation.
- Avoid introducing dependencies without reviewing their license, provenance, maintenance status, and transitive dependency tree.
- Do not copy code or documentation unless its license permits the intended use and attribution obligations are met.

## Architecture changes

Changes affecting syscall ABI, DKM ABI, filesystem format, boot protocol, process model, or cross-repository ownership should include an Architecture Decision Record (ADR) or a linked proposal.

## Commit and pull request guidance

Use descriptive commit messages. Pull requests should explain:
1. What changed and why.
2. Which repositories or interfaces are affected.
3. How the change was tested.
4. Known limitations and follow-up work.

## Licensing

Original contributions are expected to be compatible with MPL-2.0 and the repository's stated license. By submitting a contribution, you agree that it may be distributed under that repository's license. Third-party material must be identified with its source and license.
