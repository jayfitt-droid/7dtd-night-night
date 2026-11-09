# Night Night

A single-player mod for **7 Days to Die v3.4** that lets you sleep through the
night in your bedroll and wake up **Well Rested**.

> **Status: 0.1.0.** Built for v3.4 (b10) and tested in single player:
> sleeping from a bedroll and a bed, before and after midnight, refusal before
> 20:00, with an enemy nearby and on a blood moon night, the night's food and
> water cost, the Well Rested buff (including after a save and reload) and
> reloading the config.

## What it does

- Place a bedroll (any colour), look at it and **hold E**. The radial menu gets
  a new **Sleep** entry next to Take. A bed can't be picked up, so it just says
  **Press E to Sleep**.
- Choose **Sleep** and the screen fades to black. You wake at **dawn** (the
  world's dawn hour, which follows your day-length setting) and the screen
  fades back in.
- You can only sleep **from 20:00 until dawn** (`sleep_after_hour`).
- You **can't sleep with enemies nearby.** Any living zombie, bandit or hostile
  animal within **30 m** of the bed stops you (`safe_radius`), including
  zombies still asleep in a nearby POI. The message tells you how many and how
  close the nearest is. The check runs again after the fade, so something that
  walks up while you're dozing off wakes you.
- You **can't sleep through a blood moon.** Sleep is refused if any part of the
  night until dawn is blood moon time.
- **The night isn't free:** you lose 2% of your food and 2% of your water for
  each hour slept, so a full night (20:00 to 04:00) costs about 16% of each
  (`hunger_per_hour`, `thirst_per_hour`; 0 turns it off).
- You wake up **Well Rested** for **15 real minutes** (`buff_duration_minutes`):
  hunger and thirst build up **5% slower** and you earn **10% more XP**.
  Sleeping again restarts the timer; it does not stack.
- **Single player only.** The Sleep entry appears only when no other player is
  connected. A hosted game with nobody else in it counts as single player.

## Install

1. Download `NightNight-<version>.zip` from the
   [releases page](https://github.com/jayfitt-droid/7dtd-night-night/releases).
2. Unzip it into the game's `Mods` folder, so you have
   `Mods\NightNight\ModInfo.xml`.
3. Start the game **with EAC off** (the launcher's "Play without EAC" option).
   DLL mods do not load with EAC on.

Remove it by deleting `Mods\NightNight`. A save with Well Rested active keeps a
harmless leftover buff entry.

## Settings

Edit `Mods\NightNight\Config\NightNightConfig.json`, then restart the game or
type `nightnight reload` in the console (F1). A value outside its range is
ignored and the default is used; the game's log says which.

| Setting | Default | Range | What it does |
|---|---|---|---|
| `sleep_after_hour` | 20 | 0-23 | Earliest hour you can sleep; allowed from then until dawn |
| `safe_radius` | 30 | 1-200 m | Any enemy closer than this to the bed stops you sleeping |
| `hunger_per_hour` | 2 | 0-20 | Food lost per hour slept, % of max; 0 = free |
| `thirst_per_hour` | 2 | 0-20 | Water lost per hour slept, % of max; 0 = free |
| `buff_duration_minutes` | 15 | 0-240 | Well Rested length in real minutes; 0 = no buff |
| `hunger_reduction_percent` | 5 | 0-100 | Hunger builds this much slower while Well Rested |
| `thirst_reduction_percent` | 5 | 0-100 | Thirst builds this much slower while Well Rested |
| `xp_bonus_percent` | 10 | 0-500 | Extra XP while Well Rested |
| `fade_seconds` | 1.5 | 0-5 | Fade to black and back; 0 = instant |
| `debug` | false | | Extra lines in the game's log |

## Console commands

Open the console with F1. `nn` works as a short name.

- `nightnight status`: the time, dusk and dawn, the blood moon day, and whether
  you could sleep where you stand right now (and why not). Also your Well
  Rested time left and your food and water.
- `nightnight enemies [radius]`: every enemy near you, with distance, and
  whether it is a dormant sleeper.
- `nightnight reload`: re-read the config.
- `nightnight night`: set the time to the sleep hour today (for trying it out).
- `nightnight debug [on|off]`: extra log lines until the next reload.

## Compatibility

- Adds one buff (`buffNightNightWellRested`) and three cvars. Changes no vanilla
  XML. The Sleep entry is added by code to every block of class `SleepingBag`
  (all bedrolls, `bed02`, `bunkBedMade`), so other mods' bedrolls of that
  class get it too.
- Mods that change the bedroll's radial menu should still work; Night Night
  only adds an entry.
