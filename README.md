# LandBar

A lightweight BossBar that shows **who owns the [GriefPrevention](https://github.com/GriefPrevention/GriefPrevention) claim you are standing in** — or "Wilderness" when the ground is unclaimed.

- Purely event-driven: no repeating tasks, no polling.
- Runs on **Bukkit, Spigot, Paper, Purpur, Leaf and Folia**, Minecraft **1.21 and newer** (including the 26.x versions).

## Requirements

| | |
|---|---|
| Server | Bukkit, Spigot, Paper, Purpur, Leaf or Folia |
| Minecraft | 1.21 – 26.x |
| Java | 21 or newer (the version your server already requires) |
| Claims | [GriefPrevention](https://github.com/GriefPrevention/GriefPrevention) (soft dependency — without it no bar is shown) |

> **Folia:** LandBar itself is region-thread safe, but it reads claims through GriefPrevention. Use a GriefPrevention build or fork that supports Folia.

## Commands

Main command: `/landbar` (alias `/lbar`)

| Command | Permission | Description |
|---|---|---|
| `/landbar` or `/landbar toggle` | `landbar.use` | Turn your own bar on or off (remembered) |
| `/landbar on <player>` / `off <player>` | `landbar.admin` | Toggle another player's bar |
| `/landbar reload` | `landbar.admin` | Reload config and sounds, refresh bars |
| `/landbar status` | `landbar.admin` | Scheduler, GriefPrevention hook, active bars, saved toggles |
| `/landbar debug [on\|off\|verbose]` | `landbar.admin` | Diagnostics (runtime only; config is not rewritten) |

The console may use every admin sub-command.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `landbar.use` | everyone | Toggle your own bar |
| `landbar.admin` | op | Reload, debug, status, toggle other players |

## Configuration

`plugins/LandBar/config.yml` is fully commented. Highlights:

```yaml
settings:
  worlds: [world]            # worlds where the bar is shown
  default-enabled: true
  hide-in-spectator: false
  track-vehicles: true       # update the bar while riding boats / minecarts / horses
  owner-cache-seconds: 30

bossbar:
  style: SOLID               # SOLID, SEGMENTED_6/10/12/20 (Bedrock shows solid)
  claimed:
    title: "&cLand Owner: &f%owner%"
    color: RED
  wilderness:
    title: "&eWilderness"
    color: YELLOW
```

- Colours: `&c` style codes and `&#RRGGBB` hex.
- Placeholders: `%owner%`, `%status%`, `%world%`, `%player%`.
- Owner names are inserted *after* colouring, so a name can never inject colour codes.
- Sounds accept namespaced keys (`minecraft:ui.button.click`) or legacy names (`UI_BUTTON_CLICK`); `none` disables one.
- Per-player on/off choices are stored in `plugins/LandBar/players.json`.
