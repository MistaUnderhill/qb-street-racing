# QBX Street Race Script

## Features
- Multiplayer street racing from current location to configurable GPS location
- Buy-in pot / payout system - winner take all
- Leaderboard with win tracking
- Tax option for server cut
- Radial menu race start
- two racer minimum to start
- fully open and configurable

## Setup

### 1. SQL Table
Run this in your database:

```sql
UPDATE players
SET metadata = JSON_SET(
    IF(metadata IS NULL OR metadata = '', '{}', metadata),
    '$.racewins',
    0
)
WHERE JSON_EXTRACT(metadata, '$.racewins') IS NULL;
```

### 2. Add to server.cfg:
```
ensure qbx-street-racing
```

### 3. Radial Menu:
Add this to your radial menu config:
```
{
    id = "start_street_race",
    title = "Start Street Race",
    icon = "flag-checkered",
    onSelect = function()
        TriggerEvent('qbx-street-racing:startRaceRadial')
    end
}
```
### Usage
Drive near others in vehicles and use the radial menu to start a race.

Players nearby in cars will automatically be invited.

Winner receives pot after tax.

View top 10 with /raceleaderboard

### Config
Located in config.lua.
```
-- config.lua

-- Distance (in meters) from race start to checkpoint
Config.RaceDistance = 1000.0

-- Radius to check for players in vehicles near the race starter
Config.JoinDistance = 50.0

-- Buy-in settings
Config.MinBuyIn = 500
Config.MaxBuyIn = 5000

-- Tax settings (set to 0 for no tax, or a value like 0.1 for 10%)
Config.RaceTax = 0.0

-- Countdown time in seconds before race start (locked players + countdown)
Config.CountdownTime = 3

-- Timeout for racer confirmations (in seconds)
Config.ConfirmationTimeout = 30

-- Maximum number of racers allowed per race
Config.MaxRacers = 10


```
