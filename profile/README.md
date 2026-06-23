<p align="center"><img src="https://raw.githubusercontent.com/wasmdesk/brand/main/social/wasmdesk.png" alt="wasmdesk" width="640"></p>

<h1 align="center">wasmdesk</h1>
<p align="center"><strong>A WebAssembly desktop, written in pure-Go Ruby.</strong></p>

<p align="center">
  🌐 <a href="https://wasmdesk.github.io">Website</a> ·
  🖥️ <a href="https://wasmdesk.github.io">Live demo</a>
</p>

<p align="center">
  <a href="https://github.com/go-embedded-ruby/ruby"><img alt="built on go-embedded-ruby" src="https://img.shields.io/badge/built%20on-go--embedded--ruby-9B1C2E?style=flat-square"></a>
  <img alt="WebAssembly" src="https://img.shields.io/badge/WebAssembly-CGO%3D0-654FF0?style=flat-square&logo=webassembly&logoColor=white">
  <img alt="pure Ruby" src="https://img.shields.io/badge/window%20manager-pure%20Ruby-8B5CF6?style=flat-square&logo=ruby&logoColor=white">
  <img alt="License: BSD-3-Clause" src="https://img.shields.io/badge/license-BSD--3--Clause-blue?style=flat-square">
</p>

---

**wasmdesk** is a desktop environment that runs **entirely in your browser**. Its
window manager and clients are written in **pure Ruby** and run on
[go-embedded-ruby](https://github.com/go-embedded-ruby) — a pure-Go (CGO=0) Ruby
interpreter — compiled to `js/wasm`. There is no server-side code: the compositor
owns the canvas, the stacking order and input routing, and external clients each
run in their own Web Worker and paint into a `SharedArrayBuffer`.

## Repositories

| Repo | What it is |
|------|------------|
| [**wasmbox**](https://github.com/wasmdesk/wasmbox) | the **compositor + Openbox-style window manager** — pure Ruby, `//go:embed`-ed into one self-contained `.wasm`, with a `SharedArrayBuffer` external-client protocol and a live browser demo |
| [**wasmdock**](https://github.com/wasmdesk/wasmdock) | a **macOS-style dock** — a standalone wasmbox external client (Web Worker + SAB) with hover magnification and click-to-launch |

## How it fits together

- **Compositor (wasmbox).** A Wayland-inspired single-instance compositor with an
  Openbox-style window-manager policy: stacking order, click-to-focus, cascade
  placement, decorations and a `requestAnimationFrame` render loop — all pure Ruby.
- **External clients.** Step-B clients run as separate Web Worker / WASM instances
  and speak a documented `postMessage` + `SharedArrayBuffer` protocol; the dock is
  the reference external client.
- **Pure Ruby on WASM.** Everything builds on
  [go-embedded-ruby](https://github.com/go-embedded-ruby): a single static `.wasm`,
  no runtime fetch, no C toolchain, full Ruby dynamism.

Every repository is **BSD-3-Clause**.
