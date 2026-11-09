# Changelog

## 0.1.0 - 2026-11-09

First release, for 7 Days to Die v3.4 (b10). Tested in single player.

### Added

- **Sleep** in the hold-E menu of bedrolls, single player only. Beds show
  "Press E to Sleep" instead, since Sleep is their only action.
- Sleep from 20:00 until dawn; wake at the world's dawn hour.
- Refused when an enemy is within 30 m of the bed (dormant POI zombies count),
  or when any part of the night is blood moon time.
- Fade to black and back.
- Each hour slept costs 2% of food and water.
- **Well Rested** for 15 real minutes: hunger and thirst 5% slower, XP +10%.
- Every number in `Config/NightNightConfig.json`.
- Console commands: `nightnight status | enemies | reload | night | debug`.
