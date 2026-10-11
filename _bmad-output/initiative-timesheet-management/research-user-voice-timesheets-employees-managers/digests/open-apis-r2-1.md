# Digest open-apis-r2-1: user voice on weekly timesheets (open APIs)

Accessed 2026-10-11. All quotes redacted (no names/handles/links). Quotes come from WebFetch summaries of API JSON, so wording is the fetch model's extraction, not guaranteed character-exact.

Endpoints: WORKED = HN Algolia (search, search_by_date, page=1), dev.to API, Lemmy (lemmy.world /api/v3/search). BLOCKED = Stack Exchange API (api.stackexchange.com: "unable to fetch"), so workplace/pm/money/softwareengineering/hr SE not covered. Mastodon not tried (budget).

## Claims

1. C1. Filling in timesheets is widely seen as an annoying chore. Quotes: "nobody likes filling in timesheets"; "it's always an annoying thing to have to do"; "it's either this or filling out frustrating timesheets". Community: HN. Source: https://hn.algolia.com/api/v1/search_by_date?query=timesheets&tags=comment (page only). Publisher: Hacker News (Algolia). Dates: 2026-06 to 2026-09. Accessed 2026-10-11. Confidence: med. Class: employee pain. distinct_voices: 3. communities: HN (single-community).

2. C2. Workaround: build own timesheet tool or automate filling. Quotes: "decided to build our own timesheet software" (after price increases, 2026-09); "I've got an agent that fills out my timesheets by looking at git commits" (2026-08); "the logs help me fill in my time sheets" (2026-07). Also 2014 items: Skype call history to "backfill my timesheet"; spreadsheet "only five time-slots per day"; "wrote a nice interface to the awful timesheet system" (2014-12). Community: HN. Source: HN Algolia pages above. Confidence: med. Class: workaround. distinct_voices: 3 recent plus 3 older (2014, label older). communities: HN (single-community).

3. C3. Padding or implausible timesheets when work is thin or monitored. Quotes: "to look busy and make their timesheets somewhat plausible" (2026-09, HN); "record 9 hours of work on our timesheet daily" (2026-05, Lemmy); "stop people lying on timesheets" (2026-07, Lemmy). Older HN: "still putting that '8' on your timesheet" (2014-05); "I just put a much smaller number on my timesheet" (2015-04). Sources: HN Algolia; https://lemmy.world/api/v3/search (page only). Publishers: Hacker News; Lemmy (lemmy.world instance). Confidence: med. Class: behavior. distinct_voices: 3 recent. communities: HN, Lemmy (2 communities; recent, but each voice is a stray mention, so treat as weak support).

4. C4. Late or batched submission, and chasing signatures. Quotes: "I'm supposed to submit timesheets weekly, I probably do it closer to monthly" (2015-05, HN, older); "had to collect timesheets with physical signatures for medical billing... We lost real money when signatures weren't collected" (2026-06, HN); "as long as the timesheets get signed on time" (2026-07, HN). Source: HN Algolia. Confidence: low-med. Class: chasing/approval. distinct_voices: 3. communities: HN (single-community).

5. C5. Timesheet completion tied to consequences. Quotes: "you don't get paid if you don't turn in a timesheet" (2015-05, HN, older); pizza-ordering module blocked "unless your timesheet was complete for the past two months" (2014-03, HN, older); boss checks staff "get your timesheet input on time" (2014-03, HN, older). No mention of appraisal, bonus, hike or ratings in any source. Source: HN Algolia. Confidence: low. Class: consequence. distinct_voices: 3 (all old). communities: HN (single-community).

6. C6. Excel is where teams start and where it breaks down. Source: https://dev.to/taskford/when-excel-makes-time-tracking-a-nightmare-the-solutions-that-work-2ne9 . Publisher: dev.to (vendor-authored blog post, so marketing, not user voice). Date: 2025-12-04. Only excerpt seen: "Most teams begin their time tracking journey the same way. You open a blank Excel sheet". Confidence: low. Class: vendor content. distinct_voices: 1. communities: dev.to.

7. C7. Overrun hours with a budget conflict (single anecdote). Quote: "probably 130 hours on a few of these tickets... only 60 hours" and a manager "threatening to fire me" (2026-08, HN). Confidence: low. Class: consequence anecdote. distinct_voices: 1. communities: HN (single-community).

## Time figures stated

- ~10 hours: "I actually spent almost 10 hours this week" on weekly timesheet chores (HN, 2014-05, older; context unclear from extraction, so verify).
- 40 hours: "spending 40 hours gathering 4-year-old timesheets while working full-time with two children" (Lemmy, 2026-09). A one-off retrospective collation task, not a weekly figure.
- 1.5 days: filled in "1.5 days" on a timesheet for overtime (HN 2015-05, older).
- 7.5 hours/day with manual daily submission (HN 2014-06, older). 5-6 projects/clients logged per week (HN 2014-06, older). 15-minute blocks for billing (HN 2014-08, older).
- 130 vs 60 budgeted hours on tickets (HN 2026-08), not time spent on timesheets themselves.
- 55 hours logged instead of 55 minutes (HN 2026-07), an entry error.
- No hours-per-week figure for chasing or approving found.

## Patterns

- Only HN and Lemmy yielded recent (last 18 months) material; both are general tech/social communities, not HR or PM forums. Prevalence claims are not supported by two independent HR/PM communities.
- Recurring themes: filling is disliked (HN); custom tools, automation and log-based backfill as workarounds (HN); padding or "plausible" entries (HN, Lemmy).
- Most HN timesheet hits skew to 2014-2015 (older). Most were stray mentions rather than discussion of weekly workflow.

## Leads

- HN search_by_date and Lemmy results were truncated at 100k characters; remaining pages unread (offset 100000).
- The 2026-09-10 HN thread on building own timesheet software after price rises (find parent story; likely a vendor pricing thread).
- Stack Exchange data dump or a web search on workplace.SE "timesheet" as alternate route.

## Looked for and could not find

- Stack Exchange (workplace, pm, money, softwareengineering, hr): API blocked.
- Any statement of hours per week spent chasing or approving timesheets.
- Any link between late timesheets and appraisal, bonus, hike or ratings (searched HN and Lemmy; none).
- dev.to: only one article returned for the tag.
- Mastodon: not tried.
