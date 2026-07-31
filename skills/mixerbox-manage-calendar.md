---
name: Manage a Google Calendar with MixerBox Calendar
description: Authorize a Google Calendar, list calendars and events, add an event, and find free time using MixerBox Calendar.
api: openapi/mixerbox-calendar-openapi-original.json
operations: [Authorize, Logout, ListCalendar, ListEvent, AddEvent, GetFreeTime]
method: generated
generated: '2026-07-20'
---

# Manage a Google Calendar with MixerBox Calendar

MixerBox Calendar is a Google Calendar assistant. The plugin manifest declares `auth: service_http`; the user's Google account is linked through the plugin's own `Authorize`/`Logout` operations. Base URL `https://calendar.mixerbox.com`, path prefix `/api/gpt_plugins/calendar/`.

## Steps

1. **Link the account** — if calls fail as unauthorized, direct the user through `Authorize` (`GET /authorize`). Use `Logout` (`GET /logout`) to unlink.
2. **List calendars** — call `ListCalendar` (`GET /list`) to enumerate the user's calendars and their ids.
3. **List events** — call `ListEvent` (`GET /events`) to read events for today or a date range.
4. **Add an event** — call `AddEvent` (`POST /add_event`) with the event title, start and end datetime.
5. **Find free time** — call `GetFreeTime` (`GET /free`) to propose open slots before scheduling.

## Rules

- Always read (`ListEvent`) before writing to avoid double-booking, and confirm the parsed date/time with the user before calling `AddEvent`.
- `AddEvent` is the only state-changing operation; treat it as non-idempotent (no idempotency key is supported) — do not retry blindly on timeout, re-list first.
- Respect the user's timezone when constructing `EventDateTime` values.
