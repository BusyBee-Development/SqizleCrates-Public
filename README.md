# SqizleCrates

A Minecraft plugin for creating and managing customizable crates with rewards.

## Features

- **Customizable Crates**: Create multiple crates with different rewards, settings, and appearances
- **Virtual & Physical Keys**: Choose between virtual keys (stored in database) or physical key items
- **GUI Editor**: Easy-to-use in-game editor for creating and managing crates
- **Reward System**: Add items or commands as rewards with customizable appearance and enchantments
- **Permission System**: Control access to crates with permission nodes
- **Database Storage**: Persistent storage of virtual keys using SQLite
- **PlaceholderAPI Support**: Display key counts in hologram plugins with `%sqizlecrates_key_<cratename>%`

## Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/sqca give key <key_name> <player> <amount> [--debug]` | Give keys to a player | sqizlecrates.admin |
| `/sqca giveall key <key_name> <amount>` | Give keys to all online players | sqizlecrates.admin |
| `/sqca reload` | Reload configuration | sqizlecrates.admin |
| `/sqca crate create <crate_name>` | Create a new crate | sqizlecrates.admin |
| `/sqca editor` | Open the crate editor GUI | sqizlecrates.admin |

## Configuration

### Main Configuration (config.yml)

```yaml
plugin:
  language: "en"
  check-updates: true

debug: flase

database:
  enabled: true
  type: "sqlite"
  file: "crates.db"

keys:
  physical-items: false
  key-material: "TRIPWIRE_HOOK"
  key-name: "&6%key_name% Key"
  key-lore:
    - "&7Use this to open a %crate_name% crate!"
    - "&eRight-click on the crate to begin."

sounds:
  open: "BLOCK_CHEST_OPEN"
  claim: "ENTITY_PLAYER_LEVELUP"
  error: "BLOCK_NOTE_BLOCK_BASS"

gui:
  rows: 3
  filler:
    enabled: true
    material: "GRAY_STAINED_GLASS_PANE"
    name: " "
```

## ## Crate Configuration
Each crate is stored in a separate YAML file in the `plugins/SqizleCrates/crates/` folder. Here's an example structure:

```yaml
crate:
  name: "Example"
  display-name: "&eExample Crate"
  key: "Example Key"
  permission: ""
  key-required: true
  gui:
    title: "&eExample Crate Rewards"
    rows: 5
    filler:
      enabled: true
      material: "BLACK_STAINED_GLASS_PANE"
      name: " "
  sound:
    on-open: "BLOCK_ENDER_CHEST_OPEN"
    on-claim: "ENTITY_ENDER_DRAGON_GROWL"
  location:
    world: "world"
    x: 0
    y: 70
    z: 0
  rewards:
    reward1:
      slot: 10
      display:
        material: "DIAMOND"
        name: "&bDiamond Reward"
        lore:
          - "&7Win a diamond!"
      give:
        type: "item"
        item:
          material: "DIAMOND"
          amount: 1
    reward2:
      slot: 11
      display:
        material: "EXPERIENCE_BOTTLE"
        name: "&aXP Reward"
        lore:
          - "&7Get some XP!"
      give:
        type: "command"
        command: "xp add %player% 100"
```

## Usage
1. Place the plugin in your server's plugins folder
2. Start your server to generate the default configuration
3. Create a crate using `/sqca crate create <name>`
4. Use `/sqca editor` to configure your crate
5. Place the crate in the world by clicking on the block you want to be a crate
6. Add rewards to the crate using the editor by clicking the item in your inventory
7. Give keys to players using `/sqca give key <key_name> <player> <amount>`
