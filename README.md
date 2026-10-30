# OpenDrive Pilot

> Educational open-source driving-assist architecture simulator.
> **Simulation only.** Not for use on a real vehicle, not road-tested hardware, not a safety system.

## What it is

OpenDrive Pilot is a single-file, browser-based simulator that shows how the pieces of a
driver-assistance system fit together: vision, control, planning, driver monitoring, and
vehicle-bus messaging — all running as a live simulation in one dashboard.

It is reworked from the comma.ai / openpilot approach. The whole app is one file
(`index.html`, ~60 KB). There is no backend, no database, and nothing to install.

## What the simulation shows

- Live simulation dashboard (v0.9.4-openpilot)
- Front road vision feed with AI overlay (Supercombo v3.1)
- Vision inference readout (20 FPS) and model confidence
- Lead-car detection with distance, spacing, and speed offset
- Cruise controls (set speed, e.g. 65 mph) and steering torque controls
- Manual driver override (torque > 1.8 N·m overrides the autopilot safety latch)
- Driver camera + attentiveness monitor — Attentive (Eyes Ahead), Distracted
  (Looking Down/Phone), Eyes Closed / Sleeping
- Vision condition toggles — Clear / Night / Heavy Fog
- Top-down trajectory planner (MPC Planner)
- EPS torque & steering delta chart (100 Hz loop)
- SocketCAN message bus feed (can0, 500 kbps) and raw CAN packet feed
- System state display — ENGAGED (L2 AUTO)

## Tech stack

- **HTML5** — single-file app, no framework build
- **Tailwind CSS** — via CDN (`cdn.tailwindcss.com`)
- **Font Awesome 6.4** — icons, via CDN
- **Chart.js** — telemetry charts, via CDN
- **Vanilla JavaScript** — all simulation logic in-page (canvas rendering,
  state machine, CAN feed generator)
- **No build step. No npm. No backend. No API keys.**

## How to run it

**Option 1 — just open it (easiest):**

1. Download or clone this repo.
2. Double-click `index.html` — it opens in any modern browser (Chrome, Edge,
   Firefox, Safari).
3. The simulation starts on load. Use the dashboard toggles to change vision
   conditions, driver state, cruise speed, and lead-car spacing.

**Option 2 — serve it locally:**

```bash
# from inside the repo folder
python3 -m http.server 8000
```

Then open http://localhost:8000 in your browser.

**One note:** the page loads Tailwind, Font Awesome, and Chart.js from CDNs, so
you need internet for the styling and charts to look right. The simulation logic
itself is all local.

## How to use it

- Watch the vision feed and the lead-car box react as you change conditions.
- Flip the driver state to Distracted or Drowsy and watch the attentiveness
  monitor and alerts respond.
- Adjust cruise speed and spacing to see the planner and torque chart change.
- Follow the CAN bus feed to see the messages a real assist system would
  exchange (simulated — no real vehicle is connected).

## Safety framing

This is an educational simulator. It does not connect to, control, or diagnose a
real vehicle, and it has not been tested on the road. Anyone reusing this code
should keep it in simulation.
