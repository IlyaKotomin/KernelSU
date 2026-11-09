# KotoRoot KernelSU build

Based on official KernelSU v3.2.5 (`b0bc817b4e966aa6aa830834eaf6ef765d821d40`) plus the Samsung compatibility patch published by BuSung-dev/Root-My-Galaxy-Payloads (`6e3223e689688540060ddd97a0927e927bfed207`). The Samsung patch is part of this fork's source history, not a downloaded executable.

Target: SM-S931B / S931BXXS9CZE1, exact kernel `6.6.98-android15-8-pe17667d-abogkiS931BXXS9CZE1-4k`.

- `koto-s25.yml` builds the module in a digest-pinned Android 15 / 6.6 DDK, using Android clang r510928 matching the factory kernel compiler family. Manager certificate checks are unchanged and match the official Manager APK.
- `koto-userspace.yml` builds BusyBox from pinned source in our own fork, embeds our module from a specific CI run after checking SHA-256, then compiles ksud with Rust 1.99.1, Cargo.lock and NDK 28.2.13676358.
- Original ready-made BusyBox and bootctl assets are removed from the ARM64 source asset directory. Missing source-built assets must be supplied by the build workflow. bootctl is not included because this edition is for temporary LKM root, not boot-image flashing.
- No ksuinit or additional KMI modules are bundled.
- Explicit build version variables keep kernel/userspace at 32525 / 3.2.5-koto-s25 despite fork commit counts. They do not bypass version or Manager-signature checks.

The factory kernel symbol/BTF audit is in the KotoRoot application's `docs/SM-S931B-S931BXXS9CZE1.md`. Having all required symbol names is not a complete ABI proof, security audit, or guarantee of successful hardware execution.

The official KernelSU Manager is intentionally retained with its official signature at the owner's request. This source build does not require weakening Manager authentication or installing a privately signed replacement Manager.

See LICENSE for KernelSU licensing and the pinned BusyBox/SELinux/PCRE2 source repositories for their respective terms.
