# Assignment 3: Building Your Own Game Engine, Part II

A little interactive scene I extended from my Assignment 2 simulation. It's got a car cruising on its own, a stickman I can move around with the keyboard, trees, rain, and a bell tower like before. On top of that, there are now birds flying in from both sides that I can shoot, plus a health system and a game over state.

- **Part 1 — User Interaction:** You control the stickman with the keyboard. Arrow keys or A/D move him left and right, W/Up and S/Down move him up and down, and Space shoots bullets. His legs only swing when he's actually moving, and his feet flip to match the direction he's facing.
- **Part 2 — Fixed-Time Step, Variable Rendering:** The whole thing runs on a fixed 1/60s timestep so the simulation is deterministic no matter what the frame rate is. If your machine is slow, the stickman still moves at the same speed, just the rendering stutters instead of the physics going weird.

## Controls

- **Left / Right** (or **A / D**) — move the stickman horizontally
- **Up** (or **W**) — move up
- **Down** (or **S**) — move down
- **Space** — shoot bullets
- **R** — restart after game over

He wraps around the screen horizontally, so if you walk off one edge he shows up on the other.

## Gameplay

- Birds fly in from both sides and home in on the stickman. Shoot them to rack up kills.
- The stickman starts with 100 health. Each bird that reaches him costs 25 health.
- Getting hit by the car reduces health by 90.
- When health hits 0, everything freezes and a centered "GAME OVER" message appears. Press R to restart.

## Extra Credit

- **Interpolated rendering** — movement is smoothed between fixed updates, so it doesn't look all choppy even at higher refresh rates.
- **Wrap-aware interpolation** — when the guy (or car, or trees) teleports from one side to the other, it snaps clean instead of sliding across the screen. That sliding issue was driving me a little crazy.
- **Deterministic rain** — the rain respawns using a little seeded PRNG instead of `Math.random()` inside the update loop, so the whole simulation is actually deterministic.

## Notes

- There's an FPS counter, kill counter, and health readout in the top-left corner while it runs.
- I didn't use any external libraries, so there's nothing to link or include.

## Why This Structure

The fixed-timestep loop is based on the classic accumulator pattern from the Game Programming Patterns and isaacsukin articles the assignment links to. The idea is you accumulate real elapsed time, run as many fixed update steps as have accrued, then draw once with an interpolation factor for the leftover time. That's what keeps it deterministic.

## Extras

- There's no win condition yet. the kill count just keeps climbing and the game only ends when you run out of health.
- Birds only target the stickman; they don't interact with the car or anything else.

