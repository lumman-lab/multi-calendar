---
name: meetings
description: Set up a meeting with guests in a connected Outlook.com, Hotmail, Microsoft 365 or Google calendar - shown first as a draft, and made, with its invitations sent, only after the person says yes to that draft. Use for any request to book, schedule or set up a meeting or a call with other people, or to invite someone to an event.
---

# Show the meeting, then send the invitations

An event with guests is sent to every guest, from the person's own address, the moment it is made. Nothing is made until the person has seen the meeting and said yes to it.

1. Call `calendars_list` and take the account the person named, by the address it gives. Where more than one account could hold the meeting and the person named none, ask which.
2. Find the time:
   - a time the person named - read it across every calendar with `events_list` and say what it clashes with, if anything;
   - no time - search the days they named with `free_times_find`, at the meeting's length, and offer the first few.
3. Show the meeting as a draft: the account and calendar it goes in, its title, its day, start and end in the person's time zone, every guest, its place or video link - where the person named neither, the meeting_link `preferences_get` names, which the meeting is given - its notes, and that each guest will be sent an invitation. Ask whether to send it.
4. For changes, show the meeting again as changed. A yes to an earlier version is not a yes to this one.
5. Only on an explicit yes to the meeting as last shown, make it with `events_create`. Pass a guest's time zone only as the person named it, never guessed from an address. Where the answer refuses because the time falls outside a guest's working day, tell the person that guest's time as the answer gives it, and send again with unusualHoursAgreed true only on their word.

A meeting already in the calendar is treated the same way: inviting or taking off guests with `events_edit`, or moving a meeting that has guests, tells every guest, so show the change and wait for a yes first.

Examples:

- "Set up a 30-minute call with sam@example.com from my Outlook calendar on Thursday at 15:00."
- "Book an hour with anna@example.com next week, wherever all my calendars are free."
- "Invite jo@example.com to Friday's planning meeting in Google."
