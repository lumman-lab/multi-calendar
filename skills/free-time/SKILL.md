---
name: free-time
description: Find when the person is free across every connected Outlook.com, Hotmail, Microsoft 365 and Google calendar at once, within their working hours and scheduling preferences - or when everyone in one of their circles is. Use when asked when they are free, for a time to meet, or whether a day has room. Books nothing.
---

# Free time across every calendar

This skill finds time and books nothing: no event, booking link or poll is made.

1. Search with `free_times_find` over the window asked - a day, a week, the mornings of next week - at the meeting's length, narrowing by hours and weekdays where the person did. It reads every connected calendar's busy time as each provider's own free/busy shows it and keeps to the person's working hours, buffers, notice and daily maximum, so never work free time out of `events_list` instead.
2. For a time with people in one of the person's circles, find the circle with `circles_list` and search with `circles_free_times_find`. It sees only when each member is busy, never what their events say, and keeps to no one's working hours: pass the person's own from `preferences_get` as hours and weekdays, unless they named others.
3. Answer with each free stretch, earliest first, grouped by day, in the zone the answer names, the preferred part of a stretch first where it names one.
4. Then say what the search could not count. Every account or calendar under unread was not read, so its busy time may fall inside a stretch: name it, with why - an account needing reconnection is reconnected at https://lumman.co/mcp/account/multi-calendar. Name each account under cutShort too. Where narrowedBy names daysOff or fullDays, say which days had no room for that reason, so a day with no time is not read as merely busy.

Examples:

- "When am I free for an hour on Thursday across all my calendars?"
- "Find two 30-minute slots next week, mornings only, between my Outlook and Google calendars."
- "When are Tom and I both free next week?"
