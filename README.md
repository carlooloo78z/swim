# AQUA ELITE

A playable, self-contained 3D swimming game for desktop Chrome and Edge, built with Three.js, JavaScript, HTML and CSS. No account, internet connection, installation, or external assets are required to play the included build.

## Play

Double-click **PLAY AQUA ELITE.cmd**, or open **dist/index.html** in Chrome or Edge.

Choose **Quick Race**, pick an event and difficulty, meet the field, then select **Take your marks**. The home screen includes **How to play**. Settings includes optional **Training wheels** for learning the rhythm and **Automatic breathing**.

The project-root `index.html` also works after running the build. For consistent browser storage across updates, use the same file location or the local server described below. Browser storage is specific to the browser and origin. Export a backup from Settings or Records before moving the folder or clearing browser data.

## Controls

| Key | Action |
| --- | --- |
| W | Hold to kick and accelerate |
| A / D | Adjust lateral position within your lane |
| SPACE | Tap on GO to start; then time strokes in the centre green zone |
| SHIFT | Sprint, using more stamina and oxygen |
| S | Slow down and recover stamina |
| E | Breathe and surface; holding E takes repeated breaths |
| F | Queue a turn in the final 4m, or push off when stopped at the wall |
| Q | Toggle underwater swimming; each submerged segment is limited to 15m |
| C | Cycle follow, first-person, underwater, side and broadcast cameras |
| ESC | Pause / resume |

Swimmers naturally lose speed from water drag. A good stroke gives more propulsion for less stamina. Breathing adds drag briefly. Backstroke restores oxygen naturally at the surface. A turn queued near 49.35m gives the strongest push-off. Sprint in the final metres instead of exhausting yourself at the start.

Stamina is your sprint reserve. Release SHIFT and continue W with well-timed SPACE strokes to rebuild it; S recovers it faster while slowing you down. Holding SHIFT continuously drains the reserve, and sprinting gives no boost when it is empty. A low-stamina warning tells you when to release SHIFT. Players and AI use the same recovery rules at every race distance.

Starting before GO adds a 0.50-second penalty per false start. Race times include that penalty. Relay exchanges require SPACE **after** the incoming swimmer touches the wall. The exchange delay stays on the clock.

## Included gameplay

- All 17 requested events, including the full freestyle distance programme, backstroke, breaststroke, butterfly, individual medleys and three relays.
- Seven AI opponents with varied ability, acceleration, stamina, stroke efficiency and pacing strategies; five difficulty levels.
- Four distinct articulated procedural stroke animations, dives, underwater kicks, breathing, turns and finishes. IM uses butterfly, backstroke, breaststroke, freestyle. Medley relay uses backstroke, breaststroke, butterfly, freestyle.
- Four-person relay teams, with named swimmers, individual legs, exchanges and team results. You control each successive teammate.
- Three arena themes, eight-lane 50m pools, blocks, lane ropes, floor markings, spectators, officials' equipment, diving platforms and electronic timing boards.
- Animated water shaders, planar arena reflections in High mode, caustics, underwater fog, spray and bubbles, and five camera views.
- Career tiers: local, regional, national, international, World Championships and Olympic Games. Advancement requires both XP and a qualifying placement at the current tier.
- Seven solo training drills with individual feedback and permanent power, endurance or technique improvements, capped at 10.
- Standalone AI tournaments with heats, semi-finals and finals. A top-four place **and** the qualifying time are required to advance. Progress saves between rounds.
- Personal, competition, national and world record tracking; race history, reactions, splits, stroke efficiency, average speed, medals, and podium ceremonies.
- Athlete name, nation, team, cap, suit and goggle colours; XP-unlocked signature caps. Sponsorship tiers add race XP bonuses.
- Procedural water, crowd, whistles, start/finish signals and ceremony audio. Announcer commentary uses the browser's available speech voice.
- Automatic localStorage saves, JSON export/import, optional assists and a graphics performance mode.

**All benchmark world and national records are fictional and clearly labelled in the game.** Competitors and venues are fictional. This is an independent game with no official Olympic affiliation. Tournament racing is against local AI, not online multiplayer. Assisted races are marked in race history.

The game uses a simplified sports physics model and procedural characters rather than motion-captured athletes, licensed arenas, computational fluid dynamics, or photorealistic AAA assets. Relay members share their team's visual equipment. All events and career systems are playable within that scope.

## Career route

Enter a competition from Career. Finish inside the displayed placement target and reach the XP threshold for the next invitation. Training also awards XP, improves abilities and can complete the XP part of an invitation. Sponsorships unlock at 250, 700 and 1,600 XP. The Olympic career tier requires 2,200 XP plus the preceding qualification; winning there records your champion status. The standalone Olympic tournament is available from the beginning and has separate round progression.

## Build and test

Node.js 20+ is sufficient for the build and simulation tests. There are **no npm packages to install**. Three.js r160 is vendored with its MIT licence.

```powershell
cd C:\Users\carlos\Documents\AquaElite
npm.cmd run build
npm.cmd test
npm.cmd start
```

The server prints **http://127.0.0.1:4862**. It serves the built files on loopback only. Set `PORT` to use another port.

`npm.cmd run test:browser` exercises the UI and 3D renderer with an isolated headless Chrome profile via Chrome DevTools Protocol; run the local server first. It requires Chrome at the standard Windows install path and Node.js 22+ for the built-in WebSocket client. Screenshots and test reports are saved in `test-output/`. The tests never use your normal browser profile. Only `?test=1` exposes the simulation driver used by browser QA.

`npm.cmd run test:offline` opens the packaged HTML directly, without a server, and checks customisation, audio, venue changes, a complete medley relay, the podium and saved progress. Validation includes 15 simulation/progression/pacing tests, 11 browser workflow checks and 8 offline checks. Browser runs reported zero JavaScript or shader errors. `npm.cmd run test:pacing-browser` adds four checks for the exhaustion warning, steady-pace recovery, a completed 200m race and browser errors.

Version 1.0.1 fixes steady-pace stamina recovery and adds a clear prompt to release SHIFT when the reserve is low. Existing save data remains compatible. Refresh the browser after updating the files.

## Project layout

```text
src/data.js          Events, strokes, arenas, competitors and benchmarks
src/simulation.js    Fixed 120 Hz swimming, AI, timing, turns and relay model
src/world.js         Three.js venue, swimmer rigs, water, particles and cameras
src/audio.js         Procedural Web Audio and optional speech commentary
src/storage.js       Saved progression, records and tournament qualification
src/main.js          Menus, race HUD, controls and game mode integration
style.css            Responsive full-screen game interface
scripts/build.mjs    Offline static-module bundler
scripts/serve.mjs    Optional loopback HTTP server
tests/              Simulation, progression and browser checks
vendor/             Three.js r160 and its MIT licence
dist/               Ready-to-play offline game
```

If rendering fails, enable browser graphics acceleration, update the graphics driver, and try a current Chrome or Edge. If frame rate is low, select **Settings → Water & shadows → Performance**. Audio starts after the first click. Commentary availability depends on installed browser voices. Returning to the menu before a race finishes abandons that race; existing records and progression remain intact.
