## LXRCore RedM Framework — Knowledge File

<!--
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

### Overview
LXRCore is an advanced, flexible, and lightweight framework designed for the RedM platform, which supports roleplaying servers based on *Red Dead Redemption 2*. The framework provides an immersive, realistic roleplay experience aligned with the historical and Western themes of the game. Developed by **iBoss21 / The Lux Empire** for **The Land of Wolves 🐺**, LXRCore offers a streamlined approach to creating and managing roleplay servers with comprehensive features and deep customization options.

### Features
- **Roleplay-Ready Configuration:** LXRCore ships as a pre-configured, roleplay-ready setup — server owners can stand up a fully featured community with minimal effort.
- **High Performance:** Lightweight and efficient; designed to handle 300+ concurrent players with minimal server overhead.
- **Advanced Customization:** Extensive configuration options for gameplay mechanics, economy, rules, and server settings.
- **Historical Accuracy:** Built around the authentic feel of the late 19th-century American frontier, with support for deep historical roleplay.
- **Flexible Modular System:** Drop-in modules (`lxr-hunting`, `lxr-farming`, `lxr-delivery`, etc.) let administrators add, remove, or swap components at will.
- **Localization Support:** Multi-language support with dynamic variable injection for international communities.
- **Secure and Reliable:** Built-in validation, anti-exploit logic, and resource-name protection guards against common attack vectors.
- **Multi-Framework:** First-class support for LXR-Core, RSG-Core, VORP Core, RedEM:RP, QBR-Core, QR-Core, and Standalone fallback.

### Development and Ownership

LXRCore is developed and maintained by **iBoss21** under **The Lux Empire**, powering *The Land of Wolves* RedM server.

| | |
|---|---|
| **Developer** | iBoss21 / The Lux Empire |
| **Official GitHub** | [https://github.com/LXRCore](https://github.com/LXRCore) |
| **Website** | [https://www.wolves.land](https://www.wolves.land) |
| **Discord** | [https://discord.gg/CrKcWdfd3A](https://discord.gg/CrKcWdfd3A) |
| **Store** | [https://theluxempire.tebex.io](https://theluxempire.tebex.io) |

### Live Server — The Land of Wolves 🐺

LXRCore is battle-tested on *The Land of Wolves*, a whitelisted, serious hardcore RedM roleplay server.

- **Tagline:** Georgian RP 🇬🇪 | მგლების მიწა — History Lives Here!
- **Type:** Serious Hardcore Roleplay (Discord & Whitelisted)
- **Server Listing:** [https://servers.redm.net/servers/detail/8gj7eb](https://servers.redm.net/servers/detail/8gj7eb)

### Framework Priority

| Priority | Framework | Status |
|---|---|---|
| 1 | LXR-Core | ✅ Primary |
| 2 | RSG-Core | ✅ Primary |
| 3 | VORP Core | ✅ Supported |
| 4 | RedEM:RP | 🔵 Optional |
| 5 | QBR-Core | 🔵 Optional |
| 6 | QR-Core | 🔵 Optional |
| 7 | Standalone | ⚪ Fallback |

### Tebex Escrow Compliance

All paid resources are developed to be fully **Tebex escrow compliant** and are sold through the official store at [https://theluxempire.tebex.io](https://theluxempire.tebex.io). Each resource enforces resource-name protection at runtime and follows the wolves.land codebase style.

### Getting Started

```bash
# Clone into your resources/ folder
git clone https://github.com/lxrcore/lxrcore.git

# Add to server.cfg
ensure lxrcore
```

```lua
-- Access the core in your scripts
local LXRCore = exports['lxrcore']:GetCoreObject()
```

1. Visit [https://www.wolves.land](https://www.wolves.land) for downloads and documentation.
2. Follow the installation guide provided in the docs.
3. Configure the settings to fit the specific needs of your roleplay server.
4. For advanced customization, explore the modular options and localization settings.
5. Join [Discord](https://discord.gg/CrKcWdfd3A) for community support.

---

> © 2026 iBoss21 / The Lux Empire | [wolves.land](https://www.wolves.land) | All Rights Reserved
