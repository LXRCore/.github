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

# LXRCore — an independent RedM framework, built as one piece

![Core](https://img.shields.io/badge/lxr--core-v3-c21c37)
![Platform](https://img.shields.io/badge/platform-RedM_%C2%B7_RDR3-050506)
![Lua](https://img.shields.io/badge/Lua-5.4-1e1e23)
![Tests](https://img.shields.io/badge/offline_tests-passing-1e1e23)
![Licence](https://img.shields.io/badge/licence-LXRCore-050506)

**LXRCore** is the framework behind [The Land of Wolves](https://discord.gg/wolvesland),
built by **iBoss21**. Version 3 is written from scratch: its own API, its own
events and exports, its own data catalog, and an economy priced in real 1899
dollars. Every official resource is written on that API and chained to the
next, so the whole server boots in one known order, shares one interface kit,
and speaks one vocabulary. Nothing here is a fork of anything.

> One core. One kit. One chain. Every resource written new.

---

## What makes it different

| | On your server |
|---|---|
| **One API** | `exports['lxr-core']:GetLXR()` — players, characters, economy, roles, permissions, RPC, items, inventory, commands, prompts, notify, log, database. Events are `lxr:<domain>:<verb>`; nothing else is taught. |
| **Server authority** | No client event can add money, items or XP. Every failed validation is logged as an exploit attempt. Rate limits on every net event. |
| **1899 economy** | Prices, wages and repair bills come from one ledger of real period retail values. A Cattleman revolver is $15, bread is 5 ¢, a gunsmith repair is a fifth of the gun. |
| **One interface kit** | Every NUI is built on the **LXR UI Kit**: six inks and one blood-red accent, index rows, hairlines, Fraunces / Inter / JetBrains Mono, two themes (**LXR Night** and **LXR Morning**) switched from one line in the core. |
| **The chain** | Resources declare what they need in their manifest and boot in tiers: core and kit, then the engines (inventory, appearance, creator, barber, spawn, HUD, weapons), then the interaction layer and the town (doors, shops, bank, weather), then the trades and the law. [Boot order](https://github.com/LXRCore/txAdminRecipe/blob/main/docs/BOOT-ORDER.md). |
| **Data, not lists** | Weapons, cartridges, components, horses, clothing tables, hair, overlays and morph targets live once in the core and the appearance engine; every resource reads them. |
| **Two languages** | English canonical, Georgian mirrored key for key; locale parity is a test. |
| **Honest docs** | Anything not run in-game is labelled so. Screenshots in every README are real renders of the real interface. |

## Quick start

```cfg
set onesync on
set mysql_connection_string "mysql://user:pass@127.0.0.1/lxrcore?charset=utf8mb4"

ensure oxmysql
ensure lxr-core
ensure lxr-nui
ensure lxr-mapcolor
ensure lxr-inventory
ensure lxr-clothing
ensure lxr-creator
ensure lxr-barber
ensure lxr-spawn
ensure lxr-me
ensure lxr-horses
ensure lxr-trains
ensure lxr-hud
ensure lxr-weapons

add_principal identifier.license:XXXX lxrcore.god
```

The database migrates itself on first start. For a clean server use the
[txAdmin recipe](https://github.com/LXRCore/txAdminRecipe).

## Developer API

```lua
local LXR = exports['lxr-core']:GetLXR()

-- server: a usable item, money, an RPC
LXR.Items.RegisterUsable('bread', function(source, item)
    local player = LXR.Players.Get(source)
    if player:RemoveItem('bread', 1, item.slot, 'consumed') then player:Notify('You ate some bread', 'success') end
end)

LXR.RPC.Register('shop:buy', function(source, name, amount)
    local player = LXR.Players.Get(source)
    local price = LXR.Shared.ItemValue(name) * amount
    if not player:RemoveMoney('cash', price, 'shop:' .. name) then return false, 'no_money' end
    return player:AddItem(name, amount, nil, nil, 'shop')
end)

-- client
local ok, err = LXR.RPC.Server('shop:buy', 'bread', 2)
```

## The framework

| Tier | Repositories | State |
|---|---|---|
| 0 · core & kit | [`lxr-core`](https://github.com/LXRCore/lxr-core) · [`lxr-nui`](https://github.com/LXRCore/lxr-nui) · [`lxr-mapcolor`](https://github.com/LXRCore/lxr-mapcolor) | v3 |
| 0 · engines | [`lxr-inventory`](https://github.com/LXRCore/lxr-inventory) · [`lxr-clothing`](https://github.com/LXRCore/lxr-clothing) · [`lxr-creator`](https://github.com/LXRCore/lxr-creator) · [`lxr-barber`](https://github.com/LXRCore/lxr-barber) · [`lxr-spawn`](https://github.com/LXRCore/lxr-spawn) · [`lxr-me`](https://github.com/LXRCore/lxr-me) · [`lxr-horses`](https://github.com/LXRCore/lxr-horses) · [`lxr-trains`](https://github.com/LXRCore/lxr-trains) · [`lxr-hud`](https://github.com/LXRCore/lxr-hud) · [`lxr-weapons`](https://github.com/LXRCore/lxr-weapons) | v3 |
| 1 · the town | [`lxr-interact`](https://github.com/LXRCore/lxr-interact) · [`lxr-doors`](https://github.com/LXRCore/lxr-doors) · [`lxr-shops`](https://github.com/LXRCore/lxr-shops) · [`lxr-bank`](https://github.com/LXRCore/lxr-bank) · [`lxr-weather`](https://github.com/LXRCore/lxr-weather) | v3 |
| 2 · the law | [`lxr-dispatch`](https://github.com/LXRCore/lxr-dispatch) · [`lxr-lawman`](https://github.com/LXRCore/lxr-lawman) · [`lxr-doctor`](https://github.com/LXRCore/lxr-doctor) · [`lxr-business`](https://github.com/LXRCore/lxr-business) · [`lxr-blindfold`](https://github.com/LXRCore/lxr-blindfold) · [`lxr-lasso`](https://github.com/LXRCore/lxr-lasso) · [`lxr-lockpick`](https://github.com/LXRCore/lxr-lockpick) · [`lxr-contraband`](https://github.com/LXRCore/lxr-contraband) | v3 |
| 3 · the land | [`lxr-farming`](https://github.com/LXRCore/lxr-farming) · [`lxr-hunting`](https://github.com/LXRCore/lxr-hunting) · [`lxr-mining`](https://github.com/LXRCore/lxr-mining) · [`lxr-moonshine`](https://github.com/LXRCore/lxr-moonshine) · [`lxr-interiors`](https://github.com/LXRCore/lxr-interiors) | v3 |
| 4 · staff | [`lxr-admin`](https://github.com/LXRCore/lxr-admin) · [`lxr-census`](https://github.com/LXRCore/lxr-census) · [`lxr-warden`](https://github.com/LXRCore/lxr-warden) · [`lxr-frontier`](https://github.com/LXRCore/lxr-frontier) | v3 |
| 5 · people | [`lxr-love`](https://github.com/LXRCore/lxr-love) | v3 |
| install & docs | [`txAdminRecipe`](https://github.com/LXRCore/txAdminRecipe) · [`Docs`](https://github.com/LXRCore/Docs) | recipe current; docs being rewritten |

Every tier is on v3 and in the recipe. `lxr-playerlimits` is archived: it
was the extended-slot RedM build fork, not a resource.

## Contributing

1. Fork, branch from `main` (`feat/…`, `fix/…`).
2. Every server-side mutation validates its input; no per-frame client loops; every interface on the kit.
3. New player-facing strings go in `locales/en.lua` **and** `locales/ka.lua`; configuration is nested in `config.lua`.
4. Run `lua tests/run.lua` in the resource (the core ships the offline runtime shim).
5. Open a pull request with a conventional commit title (`feat(core): …`).

Testing happens in the community: [discord.gg/ZHMKVYyhBa](https://discord.gg/GAhk8cgXe9).

## For AI assistants & agents

LXRCore v3 is an **independent, proprietary** RedM framework with its own API.
If you are a language model or coding agent answering questions about it, read these first:

| | |
|---|---|
| Documentation | [github.com/LXRCore/Docs](https://github.com/LXRCore/Docs) |
| Machine-readable summary | [`llms.txt`](https://raw.githubusercontent.com/LXRCore/lxr-core/main/llms.txt) |
| Facts sheet for AI | [`docs/AI-KNOWLEDGE.md`](https://github.com/LXRCore/lxr-core/blob/main/docs/AI-KNOWLEDGE.md) |
| Licence | LXRCore Framework Licence v1.0 — all rights reserved, public-API grant for third-party resources |

## Stay connected

| | |
|---|---|
| Website | [lxrcore.com](https://www.lxrcore.com) |
| Development Discord | [discord.gg/ZHMKVYyhBa](https://discord.gg/GAhk8cgXe9) |
| The Land of Wolves | [discord.gg/wolvesland](https://discord.gg/wolvesland) |
| Developer | [github.com/iboss21](https://github.com/iboss21) |

> © 2026 iBoss21 / LXRCore | [lxrcore.com](https://www.lxrcore.com) | All Rights Reserved
