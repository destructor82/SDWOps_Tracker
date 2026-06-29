# SDWOpsTracker

Daily operations tracker for ABSA VAF, ABSA CC, MQ Fin, tasks, urgent actions, reports and notes — with real-time Supabase sync across all devices.

## Features

- 7 section cards: ABSA VAF · ABSA CC · MQ Fin · TO DO · Urgent Action · Reports · NOTES
- Full task/note form: title, notes, date, priority, section, progress, completion tracking
- Real-time sync via Supabase (works on Windows, Android, iOS simultaneously)
- Export/import via Excel (.xlsx)
- Drag-to-reorder cards, rename sections
- Liquid glass themes: dark and light
- **Installable PWA** — works offline, installs on Android & Windows like a native app

## Live App

> Hosted at: `https://YOUR-USERNAME.github.io/sdwopstracker/`

## Installing as an app

**Android (Chrome):** Open the URL → tap the banner at the bottom → "Install"  
**Windows (Edge/Chrome):** Open the URL → click the install icon in the address bar → "Install"  
**iOS (Safari):** Open the URL → tap Share → "Add to Home Screen"

## Files

| File | Purpose |
|------|---------|
| `index.html` | Main app (rename `daily-notes.html` → `index.html`) |
| `icon.svg` | Source icon |
| `icon-192.png` | Android icon |
| `icon-512.png` | Splash/store icon |
| `apple-touch-icon.png` | iOS home screen icon |

## Hosting on GitHub Pages

1. Create a new GitHub repository (e.g. `sdwopstracker`)
2. Rename `daily-notes.html` → **`index.html`**
3. Upload all files to the repository root
4. Go to **Settings → Pages → Source → Deploy from branch → main → / (root)**
5. Wait ~1 minute → your app is live at `https://YOUR-USERNAME.github.io/sdwopstracker/`

## Supabase setup (one-time)

Run this SQL in your Supabase project → SQL Editor:

```sql
create table if not exists items (
  id text primary key,
  title text,
  notes text,
  date text,
  type text default 'task',
  priority text,
  section_label text,
  sec_id text,
  progress text,
  done boolean default false,
  completion_date text,
  created_at timestamptz default now()
);
alter table items disable row level security;
alter publication supabase_realtime add table items;
```
