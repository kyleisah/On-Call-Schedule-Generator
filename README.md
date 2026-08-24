# Duty Roster — On-Call Schedule Generator

A single-file, browser-based tool for building weekly on-call rotations across multiple zones, adjusting them when conflicts come up, and exporting the result to a calendar or a spreadsheet. No backend, no build step, no accounts — open the HTML file and it runs entirely client-side.

## Why

Most on-call rotation tools are either a shared spreadsheet nobody trusts or a paid SaaS product with more configuration than a small team needs. This is the middle ground: a rotation engine with real fairness logic, calendar export, and a spreadsheet round-trip, packaged as one HTML file you can open locally, host as a static page, or hand to a teammate.

## Features

**Zones and technicians**
- Any number of custom-named zones (e.g. Central, North, South) — add, rename inline, reorder, remove, and recolor (click a zone's dot for a native color picker)
- Add technicians one at a time to a zone; the order you add them sets the rotation order
- Reorder or rename technicians inline; remove them from a zone at any time

**Rotation logic**
- Weekly rotation, Monday 12:00 AM through Sunday midnight
- Rotation length is automatic and derived from headcount — a 5-person zone rotates every 5 weeks, a 2-person zone every 2, with no manual configuration
- Pick a start date and how many weeks to generate (up to 5 years); the sidebar shows exactly what date the schedule runs through

**Handling conflicts (swaps)**
- Click any week on the duty board to reassign it
- Choose **this week only** (a one-off — the rotation resumes normally the following week) or **this week onward** (a permanent shift — that person joins the rotation cycle from that point forward)
- Pull a cover from the same zone, or borrow someone from a different zone entirely
- A **suggested cover** is offered automatically, based on how long it's been since the candidate's last on-call turn and how far out their own next natural turn is — the goal is a genuinely balanced pick, not just whoever's convenient. Odd-sized rotations surface one best pick; even-sized rotations surface two comparably balanced options to choose between. Borrowed candidates are judged against *their own* zone's rotation, not the zone being edited.
- Every active adjustment is listed under its zone with a one-click way to undo it

**Holidays**
- Track observed company holidays; edit the date or name inline at any time
- A holiday coverage table shows exactly who's on call, in every zone, for every tracked holiday

**Duty board**
- Every generated week is shown per zone in a horizontally scrollable strip
- A "Jump to current week" button snaps every zone's row back to today if you've scrolled away
- The current week is highlighted live; adjusted weeks are visually flagged

**Export**
- **.ics** — a standard calendar file, one event per technician per week, formatted as `On-Call: <Technician>:<Zone>`, importable into Google Calendar, Outlook, Apple Calendar, or any app that reads iCalendar
- **.xlsx** — a spreadsheet with Settings, Zones (including color), Technicians, Holidays, and Swaps sheets, plus a read-only full Schedule view. Columns are auto-sized so nothing clips or overlaps.
- **Restore from spreadsheet** — edit the exported .xlsx in Excel or Google Sheets (rename people, reorder rows, add zones, adjust swaps) and re-upload it to rebuild the entire setup, making the spreadsheet a genuine save/reload format, not just a one-way export

## Getting started

1. Download `oncall-schedule-generator.html`
2. Open it in any modern browser — double-click the file, or host it as a static page
3. Add a zone, add a few technicians to it, pick a start date, and the duty board fills in automatically

Nothing is saved between sessions on its own — export to .xlsx before closing the tab if you want to pick up where you left off later.

## Tech

- Plain HTML, CSS, and JavaScript — no framework, no bundler, no dependencies to install
- [SheetJS](https://sheetjs.com/) (loaded from a CDN) handles the .xlsx export/import
- All date math is done in UTC to keep week boundaries stable regardless of the browser's local timezone or daylight saving transitions

## Browser support

Works in any current version of Chrome, Firefox, Safari, or Edge. Requires JavaScript and an internet connection on first load (to fetch fonts and the spreadsheet library from their CDNs) — after that, the calendar and rotation logic run fully offline.

## Limitations

- All data lives in memory in the browser tab; refreshing the page clears it unless you've exported a spreadsheet to restore from
- The spreadsheet restore fully replaces the current setup rather than merging changes
- Not built for timezone-distributed follow-the-sun rotations — this models one rotation per zone, one shift per week

## License

MIT — do whatever you'd like with it.
