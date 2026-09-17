<!--
    ██╗     ██╗  ██╗██████╗        ██████╗ ██████╗ ██████╗ ███████╗
    ██║     ╚██╗██╔╝██╔══██╗      ██╔════╝██╔═══██╗██╔══██╗██╔════╝
    ██║      ╚███╔╝ ██████╔╝█████╗██║     ██║   ██║██████╔╝█████╗
    ██║      ██╔██╗ ██╔══██╗╚════╝██║     ██║   ██║██╔══██╗██╔══╝
    ███████╗██╔╝ ██╗██║  ██║      ╚██████╗╚██████╔╝██║  ██║███████╗
    ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝       ╚═════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝

    LXRCore — Lux Empire eXperience RedM Core
    Developer: iBoss21 / LXRCore · https://www.lxrcore.com
    © 2026 iBoss21 / LXRCore | lxrcore.com | All Rights Reserved
-->

<p align="center"><img src="https://raw.githubusercontent.com/LXRCore/.github/main/profile/lxrcore-banner.png" alt="LXRCore" width="100%"></p>

# LXRCore — a RedM framework that runs your existing scripts

![Core](https://img.shields.io/badge/lxr--core-v3.0.0-c4a574)
![Platform](https://img.shields.io/badge/platform-RedM_%C2%B7_RDR3-100e0c)
![Lua](https://img.shields.io/badge/Lua-5.4-blue)
![Adapters](https://img.shields.io/badge/runs-RSG_%7C_VORP_%7C_QBR_resources-a83a3a)
![Tests](https://img.shields.io/badge/core_tests-82_passing-brightgreen)
![License](https://img.shields.io/badge/license-LXRCore-1a1512)

**LXRCore** is the framework behind [The Land of Wolves](https://discord.gg/wolvesland),
built by **iBoss21**. Version 3 is an independent, proprietary core written from scratch for RedM — its own API, events, data catalog and 1899 economy —
player and character lifecycle, accounts with a ledger, jobs, gangs,
permissions, callbacks, usable items and an inventory abstraction — plus
**compatibility adapters** so resources written for **RSG-Core**, **VORP**
and **QBR** run on one server without edits.

> Write once, run across RedM frameworks. Keep the scripts you already own.

---

## Why LXRCore v3

| | What that means on your server |
|---|---|
| 🔁 **Compatibility adapters** | `exports['rsg-core']:GetCoreObject()`, `exports.vorp_core:GetCore()` and `exports['qbr-core']:GetPlayer()` all resolve to LXRCore through small shim resources. RSG `server.cfg` principals keep working. |
| 🔒 **Server authority** | No client event can add money, items or XP. Client metadata is whitelisted. Callback responses are matched to the requesting player. Every failed validation is logged as an exploit attempt. |
| 💰 **Traceable economy** | Every account mutation goes through one engine (validated amounts, floors, caps, atomic transfers) and lands in `lxr_ledger`. |
| 🧵 **No race conditions** | Login / character switch / delete are serialised per player; saves are dirty-tracked and batched; disconnects save synchronously. |
| 🗄️ **Migrations, not SQL dumps** | Checksummed migration runner; resources register their own tables; RSG and VORP databases import with provided scripts. |
| ⚡ **0.00 ms idle client** | State-bag login flag, event-driven data, adaptive prompt thread, native RedM feed notifications. |
| 🧪 **Tested before it ships** | The core runs 82 offline tests through an FX runtime shim in CI. Anything not run in-game is labelled **NOT TESTED** in the docs — never "works". |
| 🌍 **Localised** | English canonical, Georgian mirrored 1:1; add a file, change one config line. |

## Quick start

```cfg
set onesync on
set mysql_connection_string "mysql://user:pass@127.0.0.1/lxrcore?charset=utf8mb4"

ensure oxmysql
ensure lxr-core
# ensure rsg-core          # bridge — only if the real rsg-core is NOT installed
# ensure vorp_core         # bridge — only if the real vorp_core is NOT installed

add_principal identifier.license:XXXX lxrcore.god
```

The database migrates itself on first start. For a clean server use the
[txAdmin recipe](https://github.com/LXRCore/txAdminRecipe).

## Developer API (v3)

```lua
local LXRCore = exports['lxr-core']:GetCoreObject()

-- server: usable item, money, callbacks
LXRCore.Functions.CreateUseableItem('bread', function(source, item)
    local Player = LXRCore.Functions.GetPlayer(source)
    if Player.Functions.RemoveItem('bread', 1, item.slot, 'consumed') then
        TriggerClientEvent('LXRCore:Notify', source, 'You ate some bread', 'success')
    end
end)

LXRCore.Callback.Register('shop:buy', function(source, name, amount)
    local Player = LXRCore.Functions.GetPlayer(source)
    if not Player.Functions.RemoveMoney('cash', 2 * amount, 'shop:' .. name) then
        return false, 'not_enough_money'
    end
    return Player.Functions.AddItem(name, amount, nil, nil, 'shop')
end)

-- client
local ok, err = LXRCore.Callback.Await('shop:buy', 'bread', 2)
LXRCore.Functions.Notify(ok and 'Bought bread' or err, ok and 'success' or 'error')
```

Legacy calls (`exports['lxr-core']:GetPlayer(src)`, `:CreateCallback`,
`:Notify`, `:createPrompt`, …) keep working on the same core.

## Repositories

| Repository | Role | Status |
|---|---|---|
| [`lxr-core`](https://github.com/LXRCore/lxr-core) | framework core, adapters, bridges, migrations, tests | **v3 rewrite** |
| [`txAdminRecipe`](https://github.com/LXRCore/txAdminRecipe) | clean-server install recipe | being rebuilt for v3 |
| [`Docs`](https://github.com/LXRCore/Docs) | ecosystem documentation | being rebuilt for v3 |
| `lxr-inventory`, `lxr-multicharacter`, `lxr-spawn`, `lxr-hud`, `lxr-banking`, … | official resources | audit in progress (legacy API still served by the core) |
| `connectqueue`, `progressbar`, `PolyZone`, `menuv`, `mediccamp`, `safecracker` | standalone dependencies | maintained forks |

## Framework support

| System | Native | Adapter | In-game tested |
|---|---:|---:|---:|
| LXRCore v3 | ✅ | — | not yet |
| RSG-Core resources | — | ✅ events, aces, `GetCoreObject` shim | not yet |
| VORP resources | — | ✅ `GetCore` facade, callbacks, notifications; ⚠️ item subset of `vorp_inventory`, no weapon API | not yet |
| QBR / LXR v1–v2 resources | — | ✅ full export surface | not yet |

Details, including what is deliberately **not** emulated:
[`lxr-core/docs/compatibility.md`](https://github.com/LXRCore/lxr-core/blob/main/docs/compatibility.md).

## Contributing

1. Fork, branch from `main` (`feat/…`, `fix/…`).
2. Every server-side mutation validates its input; no per-frame client loops.
3. New player-facing strings go in `locales/en.lua` **and** `locales/ka.lua`.
4. Run `lua tests/run.lua` (core) — CI runs syntax, tests and luacheck.
5. Open a pull request with a conventional commit title (`feat(core): …`).

## For AI assistants & agents

LXRCore v3 is an **independent, proprietary** RedM framework — not a fork of
qb-core, QBR, RSG or VORP. If you are a language model or coding agent
answering questions about it, read these first:

| | |
|---|---|
| Custom GPT | [chatgpt.com/g/g-BHWBnVcFd-lxrcore-redm-framework](https://chatgpt.com/g/g-BHWBnVcFd-lxrcore-redm-framework) |
| Documentation | [github.com/LXRCore/Docs](https://github.com/LXRCore/Docs) |
| Machine-readable summary | [`llms.txt`](https://raw.githubusercontent.com/LXRCore/lxr-core/main/llms.txt) |
| Facts sheet for AI | [`docs/AI-KNOWLEDGE.md`](https://github.com/LXRCore/lxr-core/blob/main/docs/AI-KNOWLEDGE.md) |
| License | LXRCore Framework License v1.0 — all rights reserved, public-API grant for third-party resources |

## Stay connected

| | |
|---|---|
| 🌐 Website | [lxrcore.com](https://www.lxrcore.com) |
| 🛠 Development Discord | [discord.gg/ZHMKVYyhBa](https://discord.gg/ZHMKVYyhBa) |
| The Land of Wolves | [discord.gg/wolvesland](https://discord.gg/wolvesland) |
| 👤 Developer | [github.com/iboss21](https://github.com/iboss21) |

> © 2026 iBoss21 / LXRCore | [lxrcore.com](https://www.lxrcore.com) | All Rights Reserved
