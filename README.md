# Campus Abstract Simulator (校园抽象模拟器)

A text-based college life simulation game where every day is a little absurd. Attend lectures, eat mysterious duck legs, encounter strange people at the school gate, and try to survive 60 days without running out of mood, energy, or money.

The project includes two implementations that share the same story data: a **C++ console version** and an **HTML web version**.

## Play Online

Open [GitHub Pages](https://zegreen-z.github.io/EgaoCampus/) to play the web version directly in your browser. No installation required.

To play locally, open `html_version/index.html` in any browser — double-click works too.

## How It Works

You play as a college student going through four phases each day: morning class, afternoon study, evening stroll, and night in the dorm. Every choice affects your stats:

| Stat | Raise | Risk |
|------|-------|------|
| **Mood** | Duck legs, fox encounter | Absurd events, staying up late |
| **Energy** | Rest, sleep | Part-time job, seat disputes |
| **Money** | Part-time job (+¥100) | Scam links, duck legs (-¥16) |
| **Knowledge** | Attentive listening, late-night study | Skipping class |

### Events

Random events spice up campus life: the Apology Incident, Library Seat Wars, Couple Overload at the Library, the Legendary Duck Leg, the Green Duck Leg Mystery, the Fox Encounter (every 5th day), and the Online Scam.

### Quizzes

Pop quizzes on Day 30 and Day 60 test your knowledge. You need ≥28 knowledge for the first and ≥60 for the second. Passing both earns the "Scholarship" item, which blocks one scam attempt. Failing two in a row confiscates all your items and triggers the Retreat ending.

### Items

- **Knife-Shield** (durability 3) — blocks damage in the Apology and Seat events.
- **Third-Class Scholarship** — absorbs one scam attack, then gets sealed. Earned by passing both quizzes.

### Endings

| Ending | Condition |
|--------|-----------|
| Fragile Student | Energy drops to 0 |
| Financial Genius | Money drops to 0 |
| Retreat | Mood hits 0 a second time |
| Time Manager | All events completed, both quizzes passed, mood ≤ 10, energy ≤ 10 |

## Project Structure

```
EgaoCampus/
├── html_version/          # Web version (data-engine separated)
│   ├── index.html         # Game engine & UI (driver)
│   ├── story.js           # Story data as JS (loaded via <script> tag)
│   └── game_web.html      # Legacy monolithic version (v4.0, kept for reference)
├── cpp_version/           # C++ console version
│   ├── game.cpp           # Game engine (~700 lines)
│   ├── story.json         # Story data (shared with HTML version)
│   └── nlohmann/          # JSON library
└── README.md
```

The web version loads story data from `story.js` via a `<script>` tag rather than `fetch()`, so it works both on a web server and when opened as a local file (`file://` protocol).

## Tech Stack

- **C++ version**: MSVC, nlohmann/json, Windows console (requires UTF-8 BOM for Chinese literals)
- **HTML version**: Vanilla HTML/CSS/JS, no frameworks or build tools

## Recent Updates

### v5.0 — 2026-06-24

- Added pop quiz system (Day 30 & Day 60) with knowledge thresholds and multiple-choice questions
- Added "Third-Class Scholarship" item that blocks one scam, earned by passing both quizzes
- Added "Retreat" ending: second time mood hits zero triggers dropout
- Fox encounter now triggers on every 5th day (was Day 3 only, one-time)
- Time Manager ending now requires both quizzes passed
- Refactored HTML version: separated story data (`story.js`) from game engine (`index.html`)
- Fixed `fetch()` CORS error on `file://` protocol by switching to `<script src>` loading
- Fixed missing `scam.shieldText` field in story data
- Added save format upgrade for backward compatibility with older saves

## License

This is a personal project for learning and fun. Use freely.
