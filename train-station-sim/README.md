# 🚉 Terminus — Train Station Tycoon

A city-builder-style train station simulator in a single HTML file. No installs,
no dependencies — **just open `index.html` in a browser** and play.

You inherit a sleepy one-track terminus. Passengers walk in, buy a ticket, wait on
a platform and board the next train — every boarding pays you a fare. But the real
money is in the *waiting*: hungry, thirsty, bored passengers will spend at every
shop you build. Keep them happy, grow your reputation, and the crowds grow with it.

## How to play

**The core loop**
1. Passengers enter at the 🚪 door (bottom right), buy a 🎫 ticket, walk to a
   platform, and board the next train → **fare revenue**.
2. While they wait, their needs (🍔 hunger, 💧 thirst, 🚻 restroom, 😐 boredom)
   creep up. Matching amenities turn those needs into **shop revenue**.
3. Happy passengers raise your ⭐ **reputation** → bigger crowds → more of both.
4. Serving people earns **XP** → levels unlock new buildings, tracks, line
   contracts, staff and marketing.

**Easy start:** you begin with one Local track, a 4-tile platform, a ticket machine
and a bench. Follow the goal card under the map — it walks you through the early
game and pays out cash + XP for each step.

**It gets deeper as you grow:**
- **Platforms** — every 2 tiles fits 1 more train car. Longer platforms = bigger
  trains = more boardings per stop.
- **Tracks 2–4** — buy whole new lines into your station (Manage tab).
- **Line contracts** — upgrade a track from Local → Regional → Express. Higher
  fares and bigger trains, but longer waits between them and minimum platform
  lengths.
- **Fares** — a global slider. Squeeze riders for more per ticket, at the cost of
  demand and happiness.
- **Staff** — 🧹 janitors keep the station clean, 💁 attendants speed up ticket
  queues, 💂 guards keep crowds patient. All draw a daily wage.
- **Marketing** — burn $400 for a day of +50% demand.
- **Decor** — planters, fountains and the Golden Statue radiate happiness auras.
- **Rush hours** — 07:00–09:00 and 17:00–19:00 more than double traffic. Quiet
  nights barely cover upkeep.
- **Daily books** — every midnight you pay upkeep + wages and get a P&L toast.
  Go too deep into debt and the city bails you out exactly once.

**Things that make passengers angry:** long ticket queues, full trains, standing
with nowhere to sit, unmet needs, gouging fares, and a filthy station.

**Controls:** click a card, click the map to build (drag to paint platforms).
Right-click or <kbd>Esc</kbd> cancels. <kbd>Space</kbd> pauses. 🧨 Demolish
refunds 50%. The game autosaves to your browser every ~25 seconds.

## Progression at a glance

| Level | Unlocks |
|------:|---------|
| 1 | Platform, Ticket Machine, Bench, Trash Bin, Planter |
| 2 | Food Cart, Restroom |
| 3 | **Track 2**, Coffee Shop, Info Board |
| 4 | News Kiosk, Janitors, Marketing |
| 5 | Mini Market, **Regional lines** |
| 6 | Burger Bar, **Track 3**, Attendants |
| 7 | Arcade, Fountain, Security Guards |
| 8 | **Express lines**, **Track 4** |
| 9 | First-Class Lounge |
| 10 | Golden Statue |

13 goals lead from "place a bench" to the **Grand Terminus**: 85+ reputation and
200 passengers in a single day. After that, it's endless.

## Under the hood (for tinkerers)

Everything lives in `index.html` (~1,600 lines, vanilla JS + canvas):

- **Map** — a 28×16 tile grid. Tracks enter from the left and end at buffers
  (a real terminus layout); a head concourse on the right connects every
  platform; the main hall sits below.
- **Passengers** — a small finite-state machine each (enter → ticket → optional
  shop visits → platform → board), moving on BFS paths over walkable tiles.
  Small fixtures (benches, carts, machines) never block walking; big shops do,
  and placement is refused if it would trap anyone or strand a platform.
- **Demand** — spawn rate = f(level, tracks, reputation, hour-of-day, fare,
  marketing, cleanliness). Reputation is an exponential moving average of each
  served passenger's final happiness.
- **Balance knobs** — all in the constants block at the top of the script:
  `B` (building catalog), `LINES`, `LANE_COST`, `TH` (XP thresholds), `HOURF`
  (daily demand curve), `GOALS`.
