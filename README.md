# Multi Calendar

Outlook.com, Microsoft 365, Google calendars: free time, events, invitations, booking pages, polls.

Multi Calendar is a remote MCP server run by Lumman Ltd, London. It puts every calendar account you connect - Outlook.com and Hotmail, Microsoft 365 and Google, several of each - behind one connector, so an AI client can find time free in all of them in one call, read and change events, answer invitations, and hand out booking links, booking pages and group polls. This repository holds what clients install: the manifests for Claude Code, Cursor and Gemini CLI, three skills and their evals. The server itself is not in it.

## Before you start

You need a Lumman account with at least one calendar account connected - in the window your AI client opens when it first connects, or at https://lumman.co/mcp/account/multi-calendar. Sign in there with Google, Microsoft, a passkey or an emailed code. Outlook.com, Hotmail and Microsoft 365 calendars connect with Microsoft sign-in, Google calendars with Google sign-in. Each calendar account's permissions - seeing events, changing events, and inviting and replying - are set on the same page, and so are your time zone, working hours and other scheduling preferences.

## Add it to your client

### Claude

Open Multi Calendar in Claude's connectors directory, https://claude.ai/directory/connectors/lumman-multi-calendar, and press Connect. The listing connects at https://calendar.lumman.co/mcp.

### Claude Code

```
/plugin marketplace add lumman-lab/multi-calendar
/plugin install multi-calendar@multi-calendar
```

The plugin adds the connector at https://calendar.lumman.co/mcp and the three skills below. The first time a skill reaches the connector, Claude Code asks you to sign in; if it does not, run `/mcp` and choose the multi-calendar server.

### Cursor

Add the connector to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "multi-calendar": { "url": "https://calendar.lumman.co/mcp" }
  }
}
```

### VS Code

Run `MCP: Add Server`, choose `HTTP`, paste `https://calendar.lumman.co/mcp` and name it `multi-calendar`. Or add it to your user `mcp.json`:

```json
{
  "servers": {
    "multi-calendar": { "type": "http", "url": "https://calendar.lumman.co/mcp" }
  }
}
```

### Gemini CLI

```
gemini extensions install https://github.com/lumman-lab/multi-calendar
```

The extension adds the connector at https://calendar.lumman.co/mcp and the three skills below. Its first call opens Lumman's sign-in in your browser; `/mcp auth multi-calendar` opens it again.

### ChatGPT

This needs ChatGPT on the web, in a Business workspace where you are an admin or owner, or an Enterprise or Edu workspace whose role allows creating plugins with MCPs. On Pro it runs read tools alone; Plus and Free cannot add it.

1. Open chatgpt.com/plugins, press +, then Add custom MCP server.
2. Name it Multi Calendar, paste `https://calendar.lumman.co/mcp`, choose OAuth, tick the box and press Create as a plugin.
3. Install it. On the Lumman page, sign in, add a calendar if none is connected, and approve.
4. In a chat, type @ and choose Multi Calendar.

### Any other client

Add a remote MCP server at `https://calendar.lumman.co/mcp`: Streamable HTTP, OAuth 2.1 with dynamic client registration. No key or client id is needed.

## Signing in

The connector answers a client's first call with where to sign in. The client registers itself with Lumman's authorisation server and opens a Lumman page that names it: sign in, add a calendar if none is connected, and approve. Every client you approve is listed under Connected AI clients at https://lumman.co/mcp/account/multi-calendar, where its access can be taken back.

## Skills

Claude Code and Gemini CLI load three skills with the connector, and pick one by themselves when a request matches it. In Claude Code each is also a command, such as `/multi-calendar:week`.

- `free-time` - when you are free across every calendar, within your working hours, or when everyone in one of your circles is, with every calendar it could not read named. Books nothing.
- `meetings` - a meeting with guests shown to you as a draft, then made and its invitations sent only after you say yes to that draft.
- `week` - the week across every calendar, each meeting once, day by day, with clashes and unanswered invitations named. Changes nothing.

Examples:

- "When am I free for an hour on Thursday across all my calendars?"
- "Set up a 30-minute call with sam@example.com from my Outlook calendar on Thursday at 15:00."
- "What's on my calendars this week?"

## Tools

| Tool | Name |
|---|---|
| `calendars_list` | List calendars |
| `events_list` | Read events |
| `events_get` | Read an event |
| `free_times_find` | Find a time |
| `events_create` | Create an event |
| `events_edit` | Change an event |
| `events_cancel` | Cancel an event |
| `events_respond` | Answer an invitation |
| `preferences_get` | Read scheduling preferences |
| `preferences_set` | Change scheduling preferences |
| `busy_everywhere_set` | Show busy time everywhere |
| `booking_links_create` | Make a booking link |
| `booking_page_set` | Set up a booking page |
| `polls_create` | Make a group poll |
| `polls_results` | Read a poll's answers |
| `polls_book` | Book a poll's time |
| `links_polls_list` | List open links and polls |
| `links_polls_close` | Close a link or poll |
| `circles_invite` | Invite people into a circle |
| `circles_list` | List circles |
| `circles_free_times_find` | Find a time for a circle |

## Where your calendars go

Every client sends its calls to https://calendar.lumman.co/mcp, run by Lumman. Signing in runs through the authorisation server that address names. Lumman keeps no copy of your calendars: events are read from Microsoft or Google when a client asks, when a guest opens your booking page or link, when a member of your circle searches, and - where you show busy time in another calendar - by Lumman's own pass that keeps those busy blocks current. The words of every event a client reads - an invitation from a stranger included - are screened for prompt attacks by Google Cloud's Model Armor, and the events are passed on only to the client you approved. A booking link, booking page or poll keeps what it needs to offer times - its meeting's name and length, and for a poll the addresses it is for and their answers until it closes. What the connector passes on, and to whom, is in the privacy policy: https://lumman.co/privacy.

The meetings skill asks the client to show a meeting and wait for your yes. What the connector itself enforces is each calendar account's permissions, set at https://lumman.co/mcp/account/multi-calendar: with inviting and replying off, no invitation is sent from that account, whatever a client asks. A meeting at a time outside a guest's working day, where their time zone is known, is not sent until the client passes on that you agreed.

## Limits

- Your time zone is the one stored for you, taken from your device when you first connect; a client never guesses it, and asks you once where none is stored.
- Google shows an event as busy or free alone, and Outlook keeps one reminder per event.
- A Teams link is made only in a work Microsoft account, a Meet link only in a Google one. Focus time is made only in a Google Workspace account's main calendar.
- A circle finds time with people who also use Multi Calendar, and sees only when each member is busy, never what their events say.
- Each account has a daily allowance of tool calls; past it, a call is refused with the time the next one is available.
- An event whose words screen as a prompt attack is withheld rather than passed on, and a call whose screening cannot finish is closed.

## Evals

`claude plugin eval .` runs three cases, one per skill, against an invented week across an Outlook.com and a Google calendar, answered from fixed mock files under `evals/`.

To see what the skills add, every case ran in two setups with the connector's tools in place: once with the plugin as shipped, once with its `skills/` folder removed (`claude plugin eval <copy> --ablation none`). Run on 18 October 2026 with Claude Code 2.1.292, model claude-sonnet-5-5 and claude-sonnet-5-5 as the judge (`--judge-model`), three runs per case each way:

- free-time - gives Thursday's two free stretches and names the account it could not read: 3 of 3 with the skills, 2 of 3 without.
- meetings - shows the call as a draft and asks before sending the invitation: 3 of 3 with, 0 of 3 without; without the skills Claude created the event and sent the invitation at once in every run.
- week - lists each meeting once, day by day, with the clash, the unanswered invitation and the unread account: 3 of 3 with and without. The skill adds nothing measurable here.

Overall score 1.00 with the skills and 0.67 without. Three runs per case is a small sample, and the mocks answer the same whatever Claude changes.

## Security

Report a vulnerability privately through GitHub, as [SECURITY.md](SECURITY.md) describes.

## Support

Write to the address under Contact Us in Lumman's privacy policy: https://lumman.co/privacy.

## Licence

The files in this repository are under the MIT licence in [LICENSE](LICENSE). The Multi Calendar service they connect to is provided under Lumman's terms: https://lumman.co/terms.
