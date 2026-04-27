# Project Dyne: The Hybrid Evolution 🚀

**Project Dyne** is a high‑performance, hybrid operating system designed to merge the hardware versatility of the Linux kernel with the application interface (API) and aesthetic soul of **classic Mac OS X (10.3 Panther – 10.13 High Sierra)**.

Built in Rust and orchestrated by Ryan, Dyne OS aims to become the **“Fourth Pillar”** of computing—alongside Linux, macOS, and Windows—by providing a universal binary translation layer and a complete, open‑source Darwin‑compatible environment that runs on commodity x86_64, ARM64, and PowerPC (PPC) hardware.

---

## 🏛️ The Final Architecture (The Layer Cake)

Dyne is constructed as a set of independent, modular “Organs” that sit atop a minimal Linux Hardware Abstraction Layer (HAL). Every organ is a dedicated Rust workspace crate, and together they form a complete, classic Mac OS X user experience.

┌─────────────────────────────────────────┐
│ CARBON DESKTOP │ ◄── Aqua‑like environment, “Dynamic Desktop”
│ (Crimson Stable / Clover Labs) │
├─────────────────────────────────────────┤
│ DYNE CORES │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐│
│ │ DOORS │ │ FLUID │ │ PRISM ││
│ │ App Env, │ │ Graphics │ │ Audio ││
│ │ Cocoa RT │ │ Vulkanic│ │CoreAudio→││
│ │Container │ │ Wayland │ │PipeWire ││
│ └──────────┘ └──────────┘ └──────────┘│
├─────────────────────────────────────────┤
│ DYNE‑CORE KERNEL │
│ ┌─────────────────┐ ┌────────────────┐ │
│ │ ONYX │ │ LINUX KERNEL │ │
│ │Darwin/XNU │ │ (Fedora‑based│ │
│ │Mach, libsystem, │ │ HAL, drivers)│ │
│ │dyld, CF, launchd│ │ │ │
│ └─────────────────┘ └────────────────┘ │
└─────────────────────────────────────────┘


### 🧠 ONYX — The Darwin / XNU Soul (The Brain)
Onyx is a **userspace daemon** that implements the full Darwin/XNU personality for every Mac application. It provides:
- A Mach IPC daemon (ports, messages, task/thread management)
- The `libsystem` C runtime (pthreads, BSD syscall wrappers, `mach_msg`)
- The dynamic linker (`dyld`) for Mach‑O binaries
- A port of Apple’s `launchd` init system
- CoreFoundation (`CF`), Security, and IOKitUser shims
- A `binfmt_misc`‑based binary loader with native (x86_64‑on‑x86_64) and Unicorn‑based CPU emulation paths (for ARM/PPC guests)

Onyx is the single entry point for every macOS `.app` bundle; it transforms the process into a Darwin‑compatible world while the Linux kernel remains purely a HAL.

### 🚪 DOORS — Containerised Application Runtime (The Skin)
Every application runs inside its own **Door** — a Linux namespace‑isolated container. Doors combines:
- **Strong isolation:** PID, mount, network, and IPC namespaces
- **A Cocoa/Swift runtime:** A clean‑room reimplementation of AppKit, Foundation, CoreGraphics, and CoreData, built on the MIT‑licensed **Cocotron** (via Darling’s fork, `darling-cocotron`). This gives Mac apps the GUI toolkit they expect without any proprietary Apple code.
- **Declarative resource policies:** apps request only the RAM, GPU, network, and peripherals they need.

Doors is the “Xerox Rooms” philosophy brought to life — every app is a self‑contained world, managed by Onyx and drawn by Fluid.

### 🎨 FLUID ENGINE — Quartz Extreme ++ (The Eyes)
Fluid is a **Smithay‑based Wayland compositor** that replicates the full behaviour of Quartz Extreme as it existed in macOS 10.13 High Sierra. It includes:
- A CoreGraphics‑compatible 2D rendering engine (bezier paths, PDF drawing model, sub‑pixel anti‑aliasing)
- A Vulkan‑backed hardware compositor (with optional OpenGL, Metal‑via‑Vulkan, and Direct‑X gateways for Proton)
- Window management, display services, and event routing
- Dynamic desktop “Cloaks” (themes) — Carbon (default), Clover (rolling), and the hidden GRID (ENCOM OS 12 homage)

Fluid is **Quartz Extreme on steroids**: all graphics, computing, and rendering pipelines flow through a single, unified organ.

### 🔊 PRISM — CoreAudio Clone (The Ears)
Prism is a **1:1 functional clone of macOS CoreAudio**, bridged directly to the PipeWire multimedia framework. It implements:
- The full CoreAudio HAL (AudioHardware, AudioDevice, AudioStream, property listeners)
- AudioUnit host lifecycle (discovery, instantiation, format negotiation, render callbacks)
- AudioToolbox services (AudioQueue, AudioFile, AudioConverter, AUGraph)
- Zero‑latency, bit‑perfect audio routing via PipeWire’s native graph

When a Mac app calls `AudioOutputUnitStart()`, Prism translates the request into a PipeWire stream and fires the app’s IOProc with real‑time audio buffers — indistinguishable from a real Mac.

### 🖤 CARBON — The Dynamic Desktop (The Face)
The default desktop environment is named **Carbon** — an Aqua sibling and direct successor in spirit. It is a “Dynamic Desktop” that supports:
- **Cloaks** (themes) — including the stable Crimson cloak, the rolling Clover cloak, and the hidden GRID (Tron/ENCOM) Easter egg
- Fluid Engine‑powered animations, transparency, and live wallpaper blending
- A traditional spatial Finder‑like file manager

Carbon is what an Apple engineer in 2005 would have designed to succeed Aqua: dark, structural, elemental, and deeply tied to the classic OS X legacy.

---

## 🛠️ The Dev Stack
- **Architect:** Ryan — System architecture, OS design, AI orchestration
- **Language:** Rust (safety‑first, zero‑cost abstractions)
- **Editor:** Zed (the high‑performance Rust forge)
- **AI Council:**
  - **DeepSeek** — architectural consultation, code generation, and implementation
  - **Gemini** — licensing strategy, documentation, and multimodal analysis
  - *This is one of the first OS projects built with AI as a core development tool.*
- **Target Hardware:** Intel x86_64 (primary), ARM64 (Apple Silicon & Raspberry Pi), PowerPC 32/64 (G4/G5 heritage)
- **Target macOS Baseline:** macOS 10.13 High Sierra (Darwin 17.x) — the final version to support 32‑bit apps without compromise, and the peak of the “classic” Mac OS X era.

---

## 📦 The Pillage Vault (25 Forked Reference Repos)
Dyne OS is built on the shoulders of giants. All original Apple open‑source components have been forked for **clean‑room study and header reference** under their original APSL 2.0 licenses. The complete list now includes:

| Category | Repositories |
|----------|--------------|
| **Kernel & IOKit** | `XNU`, `IOKitUser` |
| **Libsystem & Runtime** | `Libsystem`, `libpthread`, `libclosure`, `DYLD` |
| **Core Services** | `CF`, `Security`, `CommonCrypto`, `configd`, `Libdispatch` |
| **Objective‑C Runtime** | `Objc4` |
| **Cocoa / AppKit (Cocotron)** | **`darling-cocotron`** (MIT‑licensed reference for AppKit, Foundation, CoreGraphics, CoreData) |
| **Base Utilities** | `system_cmds`, `shell_cmds`, `network_cmds`, `coreutils`, `gnu_bash` |
| **File System** | `HFS` |
| **Build Tools** | `cctools`, `ld64` |
| **Compatibility Bridges** | `Proton`, `Darling`, `distribution-macOS` |

**Total: 25 repositories** — the complete Darwin foundation, legally firewalled behind the APSL 2.0 window and the GPLv3 House.

---

## 🛡️ Licensing: The “GPLv3 House” with an “APSL 2.0 Window”
- **All original Dyne Rust crates (ONYX, DOORS, FLUID, PRISM, CARBON):** Licensed under **GNU GPLv3** — forever free, forever open. Any modifications must be shared back with the community.
- **Darwin Bridge Headers (Apple open‑source):** Maintained under **APSL 2.0** as reference material only. No Apple code is directly included in the GPLv3 engine.
- **Cocotron (AppKit, Foundation, CoreGraphics):** Used as an MIT‑licensed reference for clean‑room reimplementation. The MIT license is GPL‑compatible and imposes no copyleft restrictions.

This strategy guarantees that Dyne can never be locked down by a corporation, while respecting the heritage of the open‑source Darwin ecosystem.

---

## 🚀 Release Identities
- **Dyne OS 1.0 “Crimson”** — stable, polished, production‑ready (Pantone 19‑1762 TCX, hex `#9e1c3c`)
- **Dyne Labs “Clover”** — rolling/unstable, bleeding‑edge, community‑driven (Pantone 18‑2320 TCX, hex `#2a5a4c`)

---

*“Vision is the art of seeing things invisible.” – Dyne OS is the invisible made manifest.*
