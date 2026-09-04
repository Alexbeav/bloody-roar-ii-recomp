# Bloody Roar II development log

## 2026-09-03 — setup package mod catalog

The first `v0.1.1` build made all four setup packages. The workflow then
rejected each package because it contained no mod catalog. The title package
wrapper did not pass the built `mods` directory to the shared packager.

The wrapper now passes `--runtime-dir mods`. The release workflow will still
reject a package if the catalog is absent, contains machine state, or contains
a developer-only package.

Consulted leads:

- `_runs/knowledge/FINDING_CANDIDATES.md`, `PSX-PUB-001` and `PSX-PUB-016`
- `_runs/knowledge/regressions/REGRESSION_LEDGER.md`, `PSX-PUB-016`
- GitHub searches for the exact error and wrapper option; no matching result
  was indexed

The failed CI run `33743305573` is the reproduction. This correction does not
authorize a release.

## 2026-09-04 v0.1.2 POSIX setup-copy candidate

This candidate pins PSXRecomp 40ce47896026be52bcaae7de03b69766e0bd03e4 and recomp-ui be8ac1d03ee19d55394b5a5f2d9d1506edd56659.
Linux and macOS packages use native CMake, Ninja, Python, C, and C++ tools.
Windows keeps the portable toolchain route. This change does not change game
code or the graduation state. Build-only CI and every exact-package release
gate must pass before publication.
