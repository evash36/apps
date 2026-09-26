# Car Drivers

A static, single-player driving game inspired by the original hand-drawn design.

## Play

Open `index.html` in Arc or another modern browser. For consistent local storage and local development, serve this folder:

```sh
cd /Users/rahul.sharma/ai/experiments/car-drivers/game
python3 -m http.server 8080
```

Open http://localhost:8080. To play on a phone on the same trusted network, open the computer's LAN address on port 8080. Browser storage belongs to the device and website address: trophies earned from a local file will not transfer automatically to a hosted site.

## Controls

- Touch: hold the left joystick right to accelerate; left brakes; up/down steer between three lanes. Action buttons support a second simultaneous touch.
- Keyboard: right/D accelerates, left/A brakes, up/W and down/S steer, Space jumps, E toggles swimming, G toggles gliding, Escape pauses.
- Swimming prevents water-trap slowdown. Jumping and gliding avoid every trap while airborne.
- Gliding uses energy, which recharges on the ground. It needs at least 25% energy to start.
- Mud, puddles and bumps slow the car for 1.7 seconds; they never cost a life or end a level.
- The game pauses when its browser tab loses focus. Choose another road to abandon a run and restart later.

## Five levels

Original (400 m), Jiggly Road (600 m), Rainbow Road (800 m), Lakeside Splash (1,000 m), Sky Adventure (1,200 m). All are open. Each completion awards a unique, progressively more ornate trophy. Customisation and trophies save locally, when browser storage is available. No backend, tracking, external assets, accounts or purchases.

## Deploy

Upload `index.html`, `style.css`, `audio.js`, and `game.js` together to any static website host. No build command or server-side runtime is required. Set the publish directory to this `game` folder if the host deploys from the parent repository. HTTPS is recommended for a public site. No deployment was performed as part of local development.

## Files

- `game.js`: input, driving, rival AI, race results, trap collisions, Canvas rendering, trophy progression, local storage.
- `audio.js`: original synthesised sound effects and an engine tone using Web Audio.
- `style.css`: responsive menus and touch controls, including compact landscape layout.
- `index.html`: accessible menus, status and controls.

The approved design study remains in `../design-preview/`.

## Verification

The browser regression script is `tests/gameplay.cjs`. With Playwright installed in a development environment, run `node tests/gameplay.cjs` (its Chromium browser must also be installed). `TEST_BROWSER_CHANNEL` can select an installed supported test browser. The script advances animation time deterministically and checks all five level completions, persisted trophies and customisation, pausing, glide energy, water slowdown versus swimming/jumping, pointer release, and responsive width bounds. Test screenshots are local outputs and are not required for deployment.

## Racing and sound

Race three local computer-controlled cars: Pip, Ziggy and Nova. They have different speeds, change lanes and slow down on traps. Cars can pass through each other without a collision penalty. Rival movement and the race clock pause with the player. There is no online multiplayer or backend.

The HUD shows position out of four, elapsed time and the gap to the leader. Finish in any position to earn the level trophy. The finish screen shows standings at your finish; any rival still on the road is labelled “Still racing”. Best results save by highest placing, then fastest time for that placing. Race again to improve.

Sound begins after interaction with the game. The Sound on/off button is available in menus and during play, including landscape. Its setting persists. Original synthesised engine, jump, trap, swimming, gliding and finish sounds require no audio files or downloads. Audio availability depends on the browser and device sound settings; gameplay continues without it.

Additional checks: `node tests/touch.cjs` verifies simultaneous steering/jumping and touch cancellation. `node tests/racing.cjs` checks rival progression, pause, results, saved bests, audio startup and mute persistence. Browser tests verify audio generation and state, not subjective sound quality.

## Driver name

Choose a name or nickname in the garage or on the pre-race screen (up to 20 characters). The name is remembered on this browser and used in race results. Blank names default to “Driver”. Names may match rivals without changing race rankings. Trophies and personal bests belong to the browser's shared save; changing the display name does not create a separate player profile. `tests/names.cjs` checks name input, persistence, duplicate names, safe text rendering and blank fallback.
