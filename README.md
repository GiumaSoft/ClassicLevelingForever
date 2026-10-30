# ClassicLevelingForever 1.4.0

An English leveling dashboard for **WoW Forever 1.60.1**, interface **16001**,
ported from ClassicLeveling 1.4.0. It uses Forever's current item, tooltip,
spellbook and trait APIs and rejects secret values instead of inspecting them.

## Dashboard

- **XP/min (60s):** actual XP gained in the last 60 online seconds.
- **XP/hr (60m):** actual XP gained in the last 3600 online seconds.
- **Average:** session XP divided by online elapsed time, converted to minute/hour.
- Session XP, elapsed online time, current character name and level.
- **Bags (vendor):** native vendor price times item count in the backpack and four carried bags.
- **Bag change:** current carried vendor value minus the value at Reset.
- A movable and lockable 332 x 195 pixel panel, expanding to 332 x 400.

Idle online time counts; offline time does not. Settings and counters are saved
per character. Missing item prices show a partial value and wait for loading
before establishing the bag baseline. Equipped items, bank contents, auction
prices and wallet gold are excluded from bag value.

## Mob history and Forever limitations

Click **Kills/min [+]** to expand the **100 most recent recorded kills**.
Columns are **Mob | Lvl | XP@lvl | Time | XP/s**. For example, `75@7` means
75 XP received while your character was level 7. Scroll with the mouse wheel
or Up/Down. **Clear** removes the history without resetting XP or bag counters.

Forever restricts combat-log access and does not expose Classic's event reader.
The addon therefore records readable **mob XP chat messages**. Kills/min counts
those records over the last 60 online seconds. Zero-XP kills cannot be counted
through this source. A mob level is used only when public unit data can identify
it; unavailable or secret levels/identities stay **?**.

**Time** and **XP/s** remain **--** when the client does not provide the required
combat data. The addon does not substitute encounter duration or guess a kill
time. If the client exposes unrestricted combat events in the future, the
existing per-creature timing support can use them. Protected combat values are
not decoded or reconstructed.

## Equipment upgrades

A **purple border** marks currently usable estimated upgrades in native Forever
bags, including combined bags, and in the installed BetterBags Camelot edition.
Borders are mouse-transparent and do not alter item clicks or quality textures.
The meter can be hidden while borders continue to update.

The comparison uses relative class/role leveling weights and relevant weapon
DPS. Native group roles take precedence; otherwise current C_Traits ranks select
the dominant branch. Spell-to-branch facts are bundled; Talents Forever is not
required. Unknown changed spells are ignored instead of inheriting old node
ranks. Untalented characters use their class's solo leveling profile.

Rings/trinkets compare both slots and respect unique/category limits. A two-hand
replacement includes the lost offhand, and offhand weapons require trained Dual
Wield. Hunter melee and Feral weapons are scored as stat sticks. Missing equipped
item data waits for loading instead of becoming a zero-score baseline.

These are **leveling estimates**, retaining ClassicLeveling's relative weights,
not a simulation of Forever's class balance or a BiS ranking. Procs, on-use/set
bonuses, school-specific spell bonuses, resistances, stat caps, weapon speed and
ability rotations are not modeled. Supplemental flat tooltip bonuses support
English; native stats are read through C_Item. Gear is never equipped and talents
are never changed automatically.

## Commands

- `/clf` or `/classiclevelingforever`: show/hide the dashboard.
- `/clf show` / `/clf hide`: set visibility.
- `/clf lock` / `/clf unlock`: control dragging.
- `/clf center`: restore the default position.
- `/clf reset`: reset XP, bag baseline, history, kill frequency and timer.
- `/clf help`: show command help.

The previous `/flvl`, `/fl` and `/foreverleveling` aliases remain available.

## Install and existing profiles

Install **ClassicLevelingForever** in `_forever_/Interface/AddOns` and restart Forever.
Do not install the Classic Era build in this client.

The tracker uses **ClassicLevelingForeverDB** per character. The public archive
contains only the ClassicLevelingForever addon folder.

For the author's existing installation, a separate, local-only data helper loads
the previous **ForeverLevelingTrackerDB** so that XP, history and settings can be
migrated on first login. The helper creates no UI. Only a helper with the explicit
import marker is loaded; an unrelated addon named ForeverLeveling is not loaded
or imported. An existing ClassicLevelingForever profile always takes precedence.
The older ForeverLeveling route planner's **ForeverLevelingDB** is preserved and
never interpreted as XP data. No Classic Era character data is copied across,
and the installer does not edit SavedVariables files. Previous installed versions
are backed up outside Interface/AddOns.

## Validation

177 automated checks execute the actual Lua files using Lua 5.1 and mocked APIs.
They include all core XP, bag, history, timing and upgrade behavior, plus a
Forever fixture configured before addon load: restricted/absent combat log,
removed Classic events/globals, C_TooltipInfo, C_SpellBook, C_Traits, combined-bag
slot identity, secret values, profile migration and preservation of the older
planner profile. Ten additional differential scenarios compare shared behavior
directly with the current ClassicLeveling 1.4.0 source. The combat restrictions
described above remain explicit differences. Live-client behavior and appearance
still require an in-game check.

Release versions are kept aligned with ClassicLeveling. The release packager
refuses a mismatch between both TOCs and the displayed addon version.
# ClassicLevelingForever
