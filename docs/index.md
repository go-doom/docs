# go-doom documentation

**A pure-Go [DOOM](https://en.wikipedia.org/wiki/Doom_(1993_video_game)) (id Tech 1,
1993) engine** for bare-metal TamaGo + UEFI under the
[cloud-boot](https://github.com/cloud-boot) loader. It is the sibling of the
[go-quake1](https://github.com/go-quake1) family (the id Tech 1/2/3 ports).

## Fork origin

This engine is a fork of [AndreRenaud/gore](https://github.com/AndreRenaud/gore)
(commit `7dc6c654…`, 2026-05-11). `gore` is itself a Go transpilation of
[doomgeneric](https://github.com/ozkl/doomgeneric) via
[`modernc.org/ccgo`](https://gitlab.com/cznic/doomgeneric.git), then hand-cleaned.
The engine has **no CGO dependency** — standard library only — and exposes its
host bindings through a small `DoomFrontend` interface, exactly the shape needed
to wire DOOM into cloud-boot's virtio device tree. The upstream README is kept as
`README.upstream.md`.

## Why this fork exists

cloud-boot is building an OS-agnostic OCI boot architecture on TamaGo + UEFI. To
showcase Phase 3 it runs classic DOOM as the **OS payload**, with rendering,
sound and input wired straight to **virtio** devices instead of SDL / X11 / a
kernel. The fork adds:

- `backend/tamago/` — a `DoomFrontend` that drives cloud-boot's virtio-gpu,
  virtio-sound and virtio-input drivers (real wiring lands as the
  [go-virtio](https://github.com/go-virtio) sound/input sprints ship);
- `internal/embedwad/` — an `io/fs.FS` shim serving a WAD blob.

## Provable-test protocol

go-doom originated the project's **4-gate provable-test protocol** that
[go-quake1](https://go-quake1.github.io/docs/) inherits. Brand: blood-red, a
D+horns glyph (no id Software trademarked assets).

## Licensing

A **BSD-3-Clause wrapper** around the **GPL-2.0** DOOM engine code: cloud-boot
adapters and tooling are BSD-3, the ported engine retains the upstream GPL-2.0
license — see the [engine repository](https://github.com/go-doom/engine).

## Where to go next

- Source: [github.com/go-doom/engine](https://github.com/go-doom/engine)
- The shared boot architecture lives in
  [cloud-boot/docs](https://cloud-boot.github.io/docs/).
