#  Silva Cleaning

Staff scheduling and time-tracking app for a cleaning company in Ireland. It is live and in daily use at **[silvacleaning.ie](https://silvacleaning.ie)**.

Cleaners open it on their phone to see the jobs assigned to them, sign in and out at each address, record how the client paid, and upload photos of the finished work. Managers schedule the jobs, manage clients and staff, and see hours worked and money collected for the week.

## The problem it solves

Cleaners work in houses and basements where mobile signal often drops. A scheduling tool that needs a connection to record a sign-in is useless exactly when it matters. This app writes the action locally and syncs it when the signal comes back, so a shift is never lost.

## What it does

**For cleaners**
- Today view showing one job at a time, full-screen, with the rest of the route collapsible
- Sign in and sign out at each job, timestamped, working with or without signal
- Record payment as cash, transfer, or unpaid
- Attach up to 8 photos per job, compressed to about 200 KB each before upload

**For managers**
- Create and edit jobs, assign cleaners, set times and prices
- Client list with addresses, phone numbers, default price and duration
- Weekly summary: hours per staff member, money collected, payments still outstanding
- Turn booking requests from the website into scheduled jobs
- Approve or reject customer reviews before they appear on the site
- Promote a cleaner to manager, or deactivate an account

## How it is built

- **No framework.** Vanilla JavaScript, HTML and CSS, in a single-file app, mobile-first.
- **Supabase** for the backend: Postgres for data, Auth for email/password sign-in with password recovery, and Storage for the job photos behind signed URLs.
- **Row Level Security** in Postgres enforces who sees what, so a cleaner cannot read another cleaner's jobs even if they tamper with the client.
- **Offline-first.** A service worker caches the app shell. Actions taken with no connection go into a local outbox queue in `localStorage` and are replayed when the device is back online.
- **Installable.** A web app manifest makes it installable on a phone home screen and it opens like a native app.
- Hosted on GitHub Pages with a custom domain.

## Running it

The app is a static site, so any static host works.

```bash
# from the repo root
python3 -m http.server 8000
# then open http://localhost:8000/app.html
```

It needs a Supabase project with the matching tables and RLS policies to sign in.

## Status

In production for a real business. Built and maintained by [Katlyn Silva](https://github.com/katlyn-silva).
