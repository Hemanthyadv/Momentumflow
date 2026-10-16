# MomentumFlow — Master Build Specification

## Mission

Build MomentumFlow inside this repository as a complete, polished, laptop-first but mobile-responsive personal productivity command center. It helps the user set daily task targets, work in batches, record genuine active time and breaks, review pace, and stay motivated through truthful feedback and achievements.

This is not a static mockup, generic admin template, or ordinary to-do list. It must be both beautiful and functional.

## Design priority: CSS-first

Spend the overwhelming majority of visual design effort on CSS, including layout, typography, spacing, component polish, responsive behavior, themes, states, depth, and motion. “90% CSS” is a design-effort target, not a literal source line-count requirement. Maintain clean, reusable application logic.

The visual direction combines premium vibrant SaaS, tasteful gamified productivity, and selective glassmorphism. Use a coherent palette based on midnight navy, electric blue, violet, cyan, emerald, coral, and warm gold. Use accents intentionally. Avoid a childish arcade look, excessive neon, low-contrast glass, generic gray cards, default browser controls, and emoji-only iconography.

Create reusable CSS variables for colors, surfaces, text, borders, spacing, type scale, radii, shadows, glows, animation timing/easing, dimensions, breakpoints, and light/dark themes. Prefer modern typography with sensible fallbacks and consistent Lucide-style icons.

## Repository-first workflow

Inspect the existing repository, package configuration, files, and conventions before modifying it. Preserve useful work and avoid creating competing app structures. If the repository is empty, choose a maintainable stack such as React + TypeScript + Vite, custom CSS, Lucide icons, and a chart library only where useful.

Separate UI from business logic. Define typed models and reusable utilities for sessions, batches, date handling, productivity calculations, storage, and achievements.

Suggested component areas include AppShell, Sidebar, TopBar, DashboardOverview, DailyGoalCard, ActiveSessionPanel, BatchTracker, ProjectSelector, ProjectCard, FocusTimer, BreakManager, ProductivityChart, BatchHistory, AchievementPanel, LevelProgress, StreakCard, DailySummary, SettingsPanel, ThemeToggle, Modal, ToastNotification, EmptyState, and ConfirmDialog. Adapt names to the repo where needed.

## Product shell

### Sidebar
Include brand icon/wordmark, Dashboard, My Projects, Focus Session, Batch History, Analytics, Achievements, Daily Reports, Settings, a quick-start action, and profile at the bottom. Provide active navigation styling, refined hover transitions, and optional collapse. On mobile use a drawer or compact navigation.

### Top bar
Display page title/subtitle, local date, current project when relevant, optional search/quick navigation, milestone or notification indicator, theme switch, profile menu, and a quick-add/start action.

### Welcome section
Personalized greeting, current date, project context, daily objective, and a motivational line. Do not assume daypart, progress, or achievement; derive messages from actual state.

### Responsive workspace
Use a carefully aligned grid with a visually dominant goal and current-session area. Supporting analytics follow below. No horizontal overflow at desktop, tablet, or phone widths. Avoid tiny touch targets.

## Daily goal command center

A prominent goal card must show target, tasks completed, remaining tasks, goal percentage, circular or ring visualization, horizontal progress bar, current task pace, planned work duration, estimated remaining active time, and status.

Example target 1,000, completed 400, remaining 600, progress 40%.

Provide a functional Edit Goal flow with project, date, task target, preferred batch size, planned duration, optional completion deadline, and notes. Validate numeric values and update dependent metrics immediately. State labels (not started, getting started, momentum, halfway, almost there, achieved, exceeded) must be data-derived. Cap the goal-ring percentage at 100% while showing extra tasks separately.

## Projects

Support multiple independent projects, including AI video annotation, audio annotation, data labeling, AI response evaluation, quality assurance, research, coding, study, and custom work.

Each project has name, category, description, color, optional icon, daily target, default batch size, planned duration, creation date, status, and linked history.

Users can create/edit/switch/archive projects and view project-specific progress/history. Switching projects must not mix records. Archiving preserves history. Project cards should be attractive and practical.

## Batch tracking

Treat each batch as a recorded unit of work; allow any positive batch size, such as 50, 100, 200, 65, or 120.

Record a unique batch ID, project/session IDs, timestamps, active duration, pause/break intervals, tasks actually completed, planned batch size, productivity rate, seconds per task, notes, and status.

Implement working controls: Start Batch, Pause, Resume, Finish Batch, Start Break, End Break, Add Partial Progress, Edit Record, Cancel Session, and View Details.

Support Planned, In Progress, Paused, Completed, Partially Completed, and Cancelled states as appropriate. Prevent multiple active timers, duplicate completion, and accidental loss. A plan for 100 with 73 actual tasks must record 73, not claim 100. History supports search/filter/sort by project, date, and state.

## Accurate timer and sessions

Use persisted timestamps as the source of truth, never only an incrementing interval counter. Timers can be throttled when a tab is hidden or a computer sleeps.

Persist start time and pause/break intervals, and derive elapsed time on render, focus, resume, and reload. Track wall-clock elapsed time, active work, paused duration, break time, task count, and current batch duration separately.

Support start/pause/resume/break/end operations with valid state transitions. While paused or on break, active time must not grow. Recover active sessions safely after refresh. Explain/resolve edge cases rather than silently corrupting the session.

## Metrics and calculations

Use consistent reusable utility functions:
- Completed tasks = sum of valid task records for the selected project/date.
- Remaining tasks = max(0, target - completed tasks).
- Raw completion percentage = completed / target × 100, with safe zero-target handling.
- Visual progress = raw percentage capped at 100%; expose over-target tasks separately.
- Tasks per active hour = completed tasks / active work hours.
- Active seconds per task = active seconds / completed tasks.
- Batch active duration = elapsed interval minus recorded pauses and breaks.
- Estimated remaining work = remaining tasks / suitable observed task-per-hour pace.
- Estimated finish = current local time + remaining active work and optional clearly labeled break allowance.
- Planned vs actual compares active work with planned duration.
- Goal pace compares actual tasks with the target's expected cumulative progress at that local time.

Never divide by zero. If there is insufficient observation data, show “Not enough data yet.” Do not manufacture an estimate. Exclude break and pause time from active productivity rates. Clearly label active duration, wall-clock duration, and break duration.

## Live work panel

Show current batch ID/number, actual batch progress, planned size, active timer, current rate, daily progress, next milestone, and estimated remaining work. Show a single obvious action appropriate to the state: Start first batch, Resume, Complete batch, Take break, or Start next batch. Styling includes rewarding transitions, loading/disabled states, and clear keyboard focus. Do not create false urgency or pressure users to skip breaks.

## Motivation engine

Motivation must be derived from actual session state, progress, milestones, consistency, and prior performance—not random quotes.

Examples:
- Start: “One batch at a time. Let’s get moving.”
- First batch: “First batch completed. You turned intention into action.”
- 250 tasks: “250 tasks done. You’re building momentum.”
- Halfway: “Halfway there. Your effort is adding up.”
- Valid new record: “New personal best. Your recorded pace improved.”
- Behind plan: “You’re behind the original plan, but the day isn’t wasted. Reset the next milestone and continue sustainably.”
- Return from break: “Welcome back. Start with one manageable batch.”
- Goal achieved: “Daily target achieved. You followed through.”

Never announce unearned success. Avoid shaming, insults, guilt, or manipulative urgency. Celebrate real effort and consistency, and avoid repeating an identical message on every action.

## Gamification

Implement XP, levels, milestones, streaks, badges, and personal records. Award XP for eligible real batch completion and meaningful milestones. Protect against duplicates on retries/edits with an auditable ledger and idempotent event IDs. Recalculate or reconcile derived rewards if source records change.

Levels show current XP, next threshold, and progress. Example badges: First Batch, Getting Started, 100 Tasks, 500 Tasks, Daily Goal, Consistency Builder, Personal Best, Session Finisher, Seven-Day Streak, Project Milestone.

Streaks use local calendar dates and a documented qualifying activity threshold; do not count future dates. Personal records can include most tasks/day, best valid tasks/hour, productive batch, longest active session, and weekly consistency. Never reward skipping breaks or excessive hours. Use tasteful unlock animations and honor reduced-motion preferences.

## Breaks and focus

Support manual breaks and optional reminders, configurable focus and break durations, notification settings, and clear pause/resume states. Reminders are non-blocking. Ask browser notification permission only after a clear user action; fall back to in-app notices when unavailable/denied. Never force a break or mark work complete automatically. Exclude breaks from active work.

## Analytics

Provide a polished Analytics page with daily completion, weekly trend, active vs break time, tasks/hour, batch duration distribution, planned vs actual work, achievement history, project comparison, personal records, and a consistency heatmap/calendar.

Filters: Today, 7 days, 30 days, custom range, one project, all projects. Tooltips, labels, and legends must be readable and consistent. Use actual stored history. Never invent history to fill a chart; use clear empty states.

## Batch history and activity timeline

Show batch ID, project, date, tasks, active duration, breaks, rate, status, and notes. Support search, filters, sort, date selection, details, edit, and confirmed delete.

A timeline may include session started, batch finished, break started, resumed work, milestone earned, and goal reached. Use real timestamps. Editing/deleting source records must update dependent metrics and reconcile XP/achievements. Prevent duplicate counting.

## Daily report

Display target, completed/remaining tasks, percentage, active time, break time, average rate, active seconds/task, batch count, best batch, XP earned, achievements, and prior-day comparison if data exists.

Provide reflection fields: what went well, what slowed me down, what to improve, and tomorrow’s target. Persist reflections by local date. Create a concise supportive summary from real statistics and allow export. Never say the goal was achieved when it was not.

## CSS implementation requirements

CSS is a first-class deliverable. Build an extensive, organized system using logical modules or clearly separated sections: tokens, reset, typography, layout, sidebar, navigation, dashboard, cards, buttons, forms, progress, timer, batches, charts, achievements, modals, notifications, responsive rules, animation, and themes. Adapt files to the actual repository.

Global styles: box sizing, predictable defaults, typography, spacing tokens, surface/border tokens, focus states, selection, scrollbar treatment, overflow handling, and consistent transitions.

Cards: layered surfaces, subtle borders, controlled shadows, refined radii, appropriate hover lift, entrance transitions, consistent padding, and strong heading/value/supporting-text hierarchy.

Buttons: gradient primary, surface secondary, ghost, destructive, icon, loading, disabled, hover/active/focus states, and appropriate touch size.

Inputs: text/number/select/date/textarea/checkbox/switch with labels, helper text, validation/error states, disabled states, and accessible focus rings.

Progress: animated rings/bars, gradient fill, milestones, accessible labels, correct edge cases, and reduced-motion fallback.

Glass: selective backdrop-filter, solid fallbacks, readable text, and opaque enough controls. Backgrounds can use layered radial gradients and ambient glow without competing with content.

Motion: card entrances, progress changes, button responses, level-up, badge unlock, goal completion, toast, sidebar, and modal transitions. Prefer transform/opacity, avoid layout shifts and continuous distracting animation, and respect prefers-reduced-motion.

Responsive design: wide desktop, laptop, tablet, phones, narrow phones. Use Grid/Flexbox, clamp() for fluid sizing, and container queries when useful. Prevent overflow; convert tables into safe scroll regions or mobile cards. No inline-style sprawl or arbitrary duplicate values.

## Themes

Implement complete dark and light modes. Dark mode uses deep layered surfaces, restrained glow, bright readable text, and subtle borders. Light mode uses clean neutrals, dark text, visible borders, careful accents, and enough contrast. No white text on pale surfaces or very low-contrast gray labels.

All components must correctly theme: charts, tooltips, modals, inputs, dropdowns, toasts, badges, navigation, progress, empty states. Persist preference locally and optionally use system preference on first run. Visually test both themes throughout the app, not only the main page.

## Persistence and data integrity

Persist profile, theme, projects, daily goals, batches, active/paused sessions, pause/break intervals, XP ledger, achievements, streak source data, reflections, and reminder preferences.

Use a versioned storage schema. Safely handle malformed/outdated data. Do not overwrite user records with demo seeds on every load. Offer export backup, validated import, duplicate-import protection, destructive-action confirmation, and reset. Use LocalStorage for modest data or IndexedDB when justified. Be truthful that local-only storage is not cloud-synced. Never store passwords or unnecessary sensitive information. Inspect any existing backend before changing architecture.

## Profile and onboarding

Allow display name, greeting preference, avatar/initials, default batch size, planned duration, theme, and reminders. Initials avatar is sufficient; a photo is optional. Changes apply immediately and persist.

First-run flow: name, create project, set target, batch size, planned duration, then begin. Allow optional steps to be skipped. Any demo data must be explicitly enabled and labeled, with a clear reset path. Do not mix demo records with real records.

## Accessibility and performance

Use semantic HTML, keyboard navigation, visible focus, accessible labels, proper contrast, progress descriptions, modal focus handling and Escape close where appropriate, reduced-motion support, readable small-screen text, helpful errors, and touch-friendly controls. Never use color alone to communicate state.

Avoid unnecessary rerenders, expensive repeated calculations, excessive animation loops, unbounded logs, needless dependencies, duplicate CSS, dangerous broad selectors, and giant components. Use derived state and clear TypeScript types. Use consistent local-time date handling.

## Every interaction must work

Edit Goal changes the goal. Start/Pause/Resume/Finish changes real session state. Finishing a batch persists actual tasks and time. Breaks are excluded from active time. Switching projects uses correct records. Theme affects all pages. Filters change real results. Export produces a usable backup; import validates. Achievements and charts use actual records; reset requires confirmation.

Do not ship dead buttons, fake timer values, fabricated stats, or pretend functionality. Disclose any genuine limitation.

## Acceptance tests

Design: premium and cohesive; extensive reusable CSS; consistent spacing, alignment and readable typography; smooth purposeful motion; polished dark and light themes; mobile layouts without horizontal overflow; no major unstyled placeholders.

Function: create project and goal; start/pause/resume/finish batch; accurate time after reload; break excluded from active duration; correct tasks, remaining goals and estimates; real analytics; no duplicated achievements on repeated actions; persistence after closing/reopening; safe import/export; working primary controls; no major console errors.

Edge cases: zero tasks, zero goal, partial batch, multiple batches, pause/resume, break/resume, reload during session, midnight crossing, target exceeded, edited/deleted historical record, no history, theme change, mobile width, invalid import.

## Work sequence

1. Inspect the current repository and preserve useful code.
2. Establish tokens, typography, surfaces, layout, controls, themes, and motion.
3. Build shell/navigation/responsive behavior.
4. Build typed models, calculations, batches, sessions, breaks, and persistence.
5. Build dashboard, goal center, and contextual motivation.
6. Add XP, levels, streaks, and achievements.
7. Add analytics, history, reports, and reflections.
8. Refine CSS, motion, empty/loading/error states, theme contrast, responsive design, and accessibility.
9. Run available tests, lint, and production build; fix failures and test core workflows.
10. Update README with setup commands, implemented features, checks actually run, and known limitations.

Do not stop after a plan or static screenshot. Implement the working app. Do not overwrite existing functionality unnecessarily. Do not claim tests passed unless you actually ran them.

## Final experience

On opening MomentumFlow I should instantly understand today’s target, actual completion, remaining work, active time, pace, next batch, earned progress, and a sustainable next step.

Make it beautiful enough to enjoy opening daily, accurate enough to trust, encouraging enough to help me act, and maintainable enough to extend. Deliver a complete responsive application—not merely a concept or visual prototype.
