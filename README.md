# MomentumFlow

A local-first, batch-based productivity command center built with React, TypeScript, Vite, custom CSS, Lucide icons and Recharts. Track real task counts, focused work time, breaks, projects and daily progress in a responsive interface with dark and light themes.

## Run it locally

Requirements: Node.js 18+ and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite. To create a production build:

```bash
npm run build
npm run preview
```

## What is implemented

- **Dashboard:** daily target, progress ring, real task totals, active-work duration, observed tasks/hour, recent batches and weekly activity chart.
- **Projects:** create and switch projects; project-specific targets, batch sizes, project summaries, archiving and restoring. Archived project history is retained.
- **Focus sessions:** timestamp-based active timer; pause/resume; breaks excluded from active time; actual task count entry; partial/full batch saving; reload recovery through local persistence; confirmation before cancellation.
- **Batch history:** search, status filters, completed tasks, actual active duration, break duration, pace and delete-with-confirmation.
- **Analytics:** actual recorded trends, project comparison, observed pace, and personal records. No sample history is charted.
- **Achievements:** XP/levels and milestones are based on recorded work; saved event keys prevent duplicate XP on refresh.
- **Daily reports:** daily statistics, local reflections, and a text report export.
- **Settings:** editable display name, theme toggle, JSON backup export/import, and confirmed local reset.
- **Design:** custom responsive CSS, desktop sidebar/mobile drawer, charts, polished cards/controls, light/dark themes, visible focus and reduced-motion support.

## Data and privacy

Version 1 uses browser LocalStorage. Data is not cloud-synced and is available only in the browser profile where you use the app. Export a JSON backup from Settings regularly. Import validates the version/essential data shape and asks before replacing current data.

## Notes and limitations

- Goals are saved per project and local calendar date; a project's default target and batch size are used until a daily goal is customized.
- Finished batches are treated as immutable except for confirmed deletion in this version; direct edit-in-place for existing records is not yet included.
- Streaks use consecutive local calendar dates with at least one saved batch containing tasks. Streak state is derived from recorded history.
- The app includes no backend, accounts, remote synchronization, or push notifications.
- Verify locally with `npm install` and `npm run build`; this repository editing session cannot run your browser or npm build in your environment.

## Project specification

The detailed product requirements are in [`docs/MASTER-BUILD-SPEC.md`](docs/MASTER-BUILD-SPEC.md).
