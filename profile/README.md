<!--
    ██╗     ██╗  ██╗██████╗        ██████╗ ██████╗ ██████╗ ███████╗
    ██║     ╚██╗██╔╝██╔══██╗      ██╔════╝██╔═══██╗██╔══██╗██╔════╝
    ██║      ╚███╔╝ ██████╔╝█████╗██║     ██║   ██║██████╔╝█████╗
    ██║      ██╔██╗ ██╔══██╗╚════╝██║     ██║   ██║██╔══██╗██╔══╝
    ███████╗██╔╝ ██╗██║  ██║      ╚██████╗╚██████╔╝██║  ██║███████╗
    ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝       ╚═════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝

    🐺 LXRCore — The Land of Wolves RedM Framework

    ═══════════════════════════════════════════════════════════════════════════════
    SERVER INFORMATION
    ═══════════════════════════════════════════════════════════════════════════════

    Server:      The Land of Wolves 🐺
    Developer:   iBoss21 / The Lux Empire
    Website:     https://www.wolves.land
    Discord:     https://discord.gg/CrKcWdfd3A
    Store:       https://theluxempire.tebex.io

    © 2026 iBoss21 / The Lux Empire | wolves.land | All Rights Reserved
    ═══════════════════════════════════════════════════════════════════════════════
-->

# 🐺 Welcome to **LXRCore** — The Land of Wolves RedM Framework

![Version](https://img.shields.io/badge/Version-1.0.0-brightgreen)
![Build](https://img.shields.io/badge/Build-Stable-blue)
![Framework](https://img.shields.io/badge/Framework-LXRCore-blue)
![License](https://img.shields.io/badge/License-Tebex%20Escrow-orange)
![Platform](https://img.shields.io/badge/Platform-RedM-black)
![Server](https://img.shields.io/badge/Server-The%20Land%20of%20Wolves%20🐺-darkred)
![Made with ❤️](https://img.shields.io/badge/Made%20with%20❤️%20by-iBoss21-purple)
![Store](https://img.shields.io/badge/Store-theluxempire.tebex.io-green)

---

## ✨ Introduction

**LXRCore** is the **production-grade RedM framework** powering *The Land of Wolves* — a whitelisted, serious hardcore roleplay server set in the late 19th-century American frontier.

Built by **iBoss21 / The Lux Empire**, LXRCore blends **performance, modularity, and developer-friendliness** to deliver immersive RP experiences that scale to hundreds of players. Every resource ships **Tebex escrow compliant** and follows the wolves.land codebase standard.

> 🐺 Whether you're building a lightweight RP server or a fully-featured frontier economy, LXRCore is your ultimate toolkit.

---

## 📑 Table of Contents

* [🚀 Features](#-features)
* [🌐 Framework Support](#-framework-support)
* [⚙️ Quick Start](#️-quick-start)
* [📚 Documentation](#-documentation)
* [🛠 Developer API](#-developer-api)
* [🤝 Contributing](#-contributing)
* [🔥 Stay Connected](#-stay-connected)

---

## 🚀 Features

🏗️ **Modular Design** – Drop-in modules: `lxr-hunting`, `lxr-farming`, `lxr-delivery`, `lxr-proploot`, and more.
⚡ **Optimized Performance** – Handles 300+ players with minimal server overhead and client FPS impact.
🔌 **Clean API** – Simple and consistent exports for all developers, across all supported frameworks.
📦 **Inventory + Items** – Metadata support, usable items, add/remove with callbacks.
📢 **Notifications** – Unified notify system for client and server.
🌍 **Localization** – Multi-language support with dynamic variable injection.
🔒 **Secure & Reliable** – Built-in validation, anti-exploit logic, and runtime resource-name protection.
🛠 **Customizable** – Easily expand into jobs, crafting, economy, housing, and more.
👥 **Community-Driven** – Built with direct feedback from RedM developers and roleplayers.
🛒 **Tebex Escrow Compliant** – All paid assets are escrow-ready and sold through [theluxempire.tebex.io](https://theluxempire.tebex.io).

---

## 🌐 Framework Support

| Priority | Framework | Status |
|---|---|---|
| 1 | **LXR-Core** | ✅ Primary |
| 2 | **RSG-Core** | ✅ Primary |
| 3 | **VORP Core** | ✅ Supported |
| 4 | RedEM:RP | 🔵 Optional |
| 5 | QBR-Core | 🔵 Optional |
| 6 | QR-Core | 🔵 Optional |
| 7 | Standalone | ⚪ Fallback |

---

## ⚙️ Quick Start

Clone into your `resources/` folder:

```bash
git clone https://github.com/lxrcore/lxrcore.git
```

Add to your **server.cfg**:

```cfg
ensure lxrcore
```

Access the core in your scripts:

```lua
local LXRCore = exports['lxrcore']:GetCoreObject()
```

✅ Done. You can now build on **LXRCore**.

---

## 📚 Documentation

Check the **developer docs** to explore:

* API usage and examples
* Usable items & inventory integration
* Server ↔ client callbacks
* Multi-framework event naming conventions
* Tebex escrow compliance guidelines

📖 [wolves.land Documentation](https://www.wolves.land)

---

## 🛠 Developer API

**Register Usable Item**

```lua
LXRCore.Functions.RegisterUsableItem("bread", function(data)
    LXRCore.Functions.RemoveItem(data.source, "bread", 1)
    Notify({ source = data.source, text = "You ate bread.", time = 4000, type = "success" })
end)
```

**Trigger Callback**

```lua
LXRCore.Functions.TriggerServerCallback("GetPlayerStats", function(stats)
    print("Cash: " .. stats.cash)
end)
```

**Progress Bar**

```lua
LXRCore.Functions.Progress("Crafting...", 5000, function()
    print("Done crafting!")
end)
```

---

## 🤝 Contributing

We ❤️ community contributions. Here's how to help:

1. Fork the repo
2. Create your branch: `feature/my-feature`
3. Commit with clear messages
4. Submit a PR

Check our [issues](https://github.com/LXRCore/.github/issues) for tasks to pick up.

---

## 🔥 Stay Connected

| | |
|---|---|
| 🌐 **Website** | [wolves.land](https://www.wolves.land) |
| 🗣️ **Discord** | [discord.gg/CrKcWdfd3A](https://discord.gg/CrKcWdfd3A) |
| 🛒 **Store** | [theluxempire.tebex.io](https://theluxempire.tebex.io) |
| 🐙 **GitHub** | [github.com/LXRCore](https://github.com/LXRCore) |
| 👤 **Developer** | [github.com/iboss21](https://github.com/iboss21) |

---

> 🐺 *With **LXRCore**, you're not just running a framework — you're building the future of RedM roleplay on The Land of Wolves.*
> Let's create something legendary 🚀

---

> © 2026 iBoss21 / The Lux Empire | [wolves.land](https://www.wolves.land) | All Rights Reserved
