# Life Countdown Calculator

An interactive life expectancy countdown calculator that visualizes how much time you have remaining based on your demographics, lifestyle, and health factors.

## What it does

The calculator asks 18 questions about your demographics, lifestyle, and health, then estimates your life expectancy using publicly available data (WHO life expectancy by country and gender) adjusted for lifestyle factors like smoking, exercise, diet, sleep, stress, and social connections.

The result is displayed across three views:

1. **Countdown** - Digital LCD-style counter showing years, days, hours, minutes, and seconds remaining. Below the counter, five stopwatch-style progress bars show time remaining within each clock cycle (years out of total life, days out of 365, hours out of 24, etc.).

2. **Your life** - A zoomable grid inspired by Tim Urban's "Your Life in Weeks" visualization. Switch between Years, Months, and Weeks views to see your entire life as a grid of cells. Past time is filled, current period is highlighted, future is empty. Supports life phases (Childhood, School, Career, etc.) with custom color coding, drill-down on click, hover tooltips, and keyboard navigation.

3. **Key factors** - All 18 questions with inline editing. Click the edit icon next to any answer to update it. The countdown recalculates immediately. Includes a Restart button at the bottom to clear all answers and start over.

## Tech stack

- Single HTML file with vanilla JavaScript
- No build step or dependencies
- All data stored in browser localStorage
- Renders 100% client-side

## Running it

Just open `index.html` in a browser. That's it.

For local development with hot reload:

```bash
npx serve .
```

Then visit the URL shown in your terminal.

## File structure

```
life-countdown/
├── index.html          The entire app (HTML, CSS, JS)
├── README.md           This file
├── CLAUDE.md           Context for Claude Code
└── package.json        Optional, for npm scripts
```

## Key design decisions

**Why a single file?** The app is small enough that splitting into separate files adds complexity without benefit. Easy to deploy anywhere, no build step needed.

**Why localStorage?** The data is personal and doesn't need a server. localStorage persists across sessions and keeps everything private to the user's browser.

**Why no framework?** Vanilla JS keeps the bundle small and the code transparent. No abstractions to learn, just DOM manipulation.

**Why Tim Urban's grid?** The "Your Life in Weeks" pattern is the most emotionally effective way to visualize mortality. Seeing your entire finite life as a grid of cells creates an impact that no number on its own can match.

## Customization notes

The life expectancy calculation in `calculateResults()` uses simple multipliers per answer. The base expectancy comes from `lifeExpectancyByCountry` and is adjusted by lifestyle factors. These adjustment values are not based on rigorous medical research and should not be treated as a real prediction. They produce a plausible estimate for reflection purposes only.

Life phases are stored separately in localStorage under `lifePhases`. Default phases are Childhood (0-5), School (6-18), and Career (23-65). Users can add, edit, and delete phases freely.

## Known limitations

- The calculation is not medically accurate. It's meant for reflection, not actual life expectancy prediction.
- Currency in questionnaire uses imperial units (lbs, inches). Metric support would require updating the BMI calculation and the question prompts.
- Weeks grid uses 52 weeks per year (loses ~1 day per year over a lifetime, but visually negligible).
- The grid view's drill-down (year → months → days) is one-way navigation; the breadcrumb is the only way back up.
