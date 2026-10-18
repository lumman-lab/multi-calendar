---
name: week
description: An overview of the week, or of any run of days, across every connected Outlook.com, Hotmail, Microsoft 365 and Google calendar - each meeting once, day by day, with clashes, unanswered invitations and anything that could not be read named. Use when asked what is on, what the week looks like, or for a summary of the calendars. Changes nothing.
---

# The week across every calendar

This skill reads and changes nothing: it answers no invitation and moves or cancels nothing.

1. Read the week with one `events_list` call across every calendar - from Monday to the Monday after, in the person's time zone - unless the person named other days.
2. Before answering, read on each calendar named under cutShort, passing its continueAt with its account and calendarId and the same period: the week is not whole until each has been read to its end. Where the answer counts events under leftOut, read the period it names again, a day or a calendar at a time, for the same reason.
3. Read the answer as it is meant:
   - an event held in several accounts answers once, naming each copy - count it once;
   - Lumman's own busy copies come apart from events, under busyCopies: they mirror busy time from another account, so never list one as a meeting;
   - an all-day event's end is the day after its last.

Answer day by day, earliest first, in the zone the answer names:

- each meeting - its time, its title, the accounts holding it, and its join link where it has one;
- clashes - two meetings holding the same time, both named;
- invitations not yet answered - who sent it and when it is;
- a day with nothing on, said in a word.

Then name every account or calendar under unread, with why, and every event under withheld: the overview is missing them.

Examples:

- "What's on my calendars this week?"
- "Give me an overview of next week across Outlook and Google."
- "Anything clashing on Wednesday?"
