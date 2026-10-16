# MomentumFlow

A personal productivity command center for batch-based work, accurate time tracking, daily targets, and encouraging progress analytics.

## Vision

MomentumFlow turns large targets into manageable batches. Set a goal such as 1,000 tasks, work in batches of 100 (or any custom size), record real task counts and active time, take breaks, and see trustworthy progress with supportive motivation.

The interface should combine premium SaaS polish, vibrant gradients, tasteful glassmorphism, and lightweight gamification — while remaining readable, responsive, and practical.

## Product principles

- **Real data only:** no fake analytics, XP, streaks, or achievements.
- **Accurate time:** use timestamps and recorded pause/break intervals, not an incrementing counter as the source of truth.
- **Encouraging, not shaming:** help users reset plans when they fall behind.
- **Local-first:** persist progress on this device and offer validated export/import backups.
- **CSS-first craft:** make the design system, responsive layout, and interaction styling a primary priority.
- **Accessible by default:** keyboard focus, sensible contrast, semantic controls, and reduced-motion support.

## Core features

- Personal dashboard with daily goal, progress ring, completed/remaining tasks, current pace, and estimated remaining work time.
- Multiple projects for AI video/audio annotation, data labeling, AI response evaluation, QA, research, coding, study, or custom work.
- Batch workflow: start, pause, resume, partial progress, complete, edit, and cancel safely.
- Work session and break tracking with elapsed time recovered correctly after reload.
- Calculated productivity metrics: tasks/hour, active seconds/task, batch duration, goal pace, and estimates when sufficient data exists.
- XP, levels, achievements, streaks, milestones, and personal records derived from actual records with duplicate-award protection.
- Analytics, batch history, filters, daily summaries, reflections, and exports.
- Complete dark/light themes, local persistence, responsive desktop/mobile layouts, and first-run onboarding.

## Suggested technology

Inspect the repository before choosing the implementation. If it is empty, a good default is React + TypeScript + Vite, custom CSS modules or organized CSS files, Lucide icons, and a chart library only where useful. Use LocalStorage for modest settings/data or IndexedDB if the record volume warrants it.

## Development acceptance criteria

- Every visible control performs its advertised action.
- Task counts and time calculations are consistent across dashboard, history, analytics, and reports.
- Break and paused time are excluded from active work rates.
- A refresh/reopen does not corrupt an active session.
- Theme, project, and data preferences persist.
- Import validates the payload and avoids duplicate records; destructive actions require confirmation.
- Empty states never invent historical data.
- Test zero targets, partial batches, pause/resume, breaks, reload recovery, midnight rollover, goal exceeded, record editing/deletion, invalid imports, both themes, and narrow screens.
- Run lint/tests/build where configured and report only checks actually completed.

## Implementation workflow

1. Inspect the current repo and preserve useful work.
2. Create the design tokens, typography, surfaces, responsive layout, themes, controls, and motion rules.
3. Build the app shell and main dashboard.
4. Implement typed data models, calculations, batch/session state, persistence, and validation.
5. Add project management, achievements, analytics, history, and daily reports.
6. Verify responsive behavior, accessibility, theme contrast, timer recovery, and core workflows.
7. Update this README with setup instructions, implemented features, and known limitations.

## Local development

Setup commands will be documented here after the app framework is added.

## Status

Initial project brief. The functional application has not yet been implemented.
