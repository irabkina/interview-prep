# System design

## Choosing prompts
Use classic, open-ended prompts and keep them vague at the start ("Design a URL shortener"), so that scoping the problem is part of the test. Examples by theme:
- Read-heavy / caching: URL shortener, news feed, typeahead
- Write-heavy / ingestion: metrics or logging pipeline, rate limiter, web crawler
- Real-time: chat, notifications, live location tracking
- Storage / consistency: key-value store, distributed file storage, payment system
- Coordination: job scheduler, distributed lock, leaderboard

For a design redo, choose a different prompt that puts weight on the same skill. If they struggled with fan-out for a news feed, the redo could be a notification system or a follower-based activity stream. Don't reuse the prompt itself.

Topic coverage for plans and lessons: requirements & estimation, API design, data modeling and SQL vs NoSQL, caching, sharding/partitioning, replication & consistency, queues & streams, load balancing, rate limiting, idempotency & retries, observability, failure modes.

Calibrate to the role's level in `role.md` (or `profile.md` if there's no role). Senior and staff candidates are expected to drive the conversation, bring up tradeoffs on their own and go deep without prompting.

## The design workspace

The user writes the design in `sessions/YYYY-MM-DD-<slug>/design.md`, open in their IDE, so they build the habit of producing a structured artifact the way they would on a whiteboard or in a shared doc. Create it with the prompt at the top and empty section headings:

```markdown
# Design: <prompt>
## Requirements (functional / non-functional)
## Estimates
## API
## Data model
## High-level design
<!-- components and data flow; an ASCII sketch or a Mermaid diagram is fine -->
## Deep dives
## Tradeoffs & open questions
```

In a mock, drop the headings if the role's format is a blank whiteboard, because structuring it themselves is part of what's evaluated. In a drill, the headings are the scaffold.

The file belongs to the user. Don't write their design for them, and don't draw their diagram. Re-read it every time they message you, so your questions follow what they've actually written. The conversation itself (clarifying questions, pushback, curveballs) happens in chat.

## Lessons and drills

A design lesson takes one concept (consistent hashing, write-ahead logs, fan-out on write vs fan-out on read…). It explains what problem the concept solves, the alternatives and when to use each, and the numbers that matter (latency of a cache vs disk vs a cross-region call). It goes in `lesson.md`, and leads straight into a drill that uses it.

Design drills are shorter and narrower than mocks. Have the user design one component in depth ("design just the storage layer for a chat app"), or run estimates for 15 minutes. Coach as they go. Ask "why that choice?", offer alternatives they haven't considered, and let them revise `design.md`.

## Mock format
- Default: 45–60 minutes. A good pacing target: about 5 minutes on requirements, about 5 on estimates, about 15 on high-level design, about 20 on deep dives, then wrap up. Tell them the time at checkpoints.
- When they ask about scope, answer like a product-minded interviewer. Supply numbers if they ask (DAU, QPS, data size), or ask them to estimate.
- When they finish the high-level design, pick 1–2 areas to dig into. Choose the weakest or most interesting parts, not the ones they're clearly comfortable with.
- Inject at least one curveball: a hot key, a region outage, 10x growth, a new requirement.

## Mock debrief rubric (score 1–4 each)
| Dimension | 4 looks like |
|---|---|
| Requirements & scoping | Separated functional from non-functional requirements, made reasonable estimates, scoped the problem explicitly |
| High-level design | Coherent components and data flow, clear APIs and data model, no obvious single points of failure left unaddressed |
| Deep dive & tradeoffs | Justified choices against alternatives, quantified where possible, handled the curveball well |
| Communication & driving | Structured, kept time, checked in with the interviewer, led the conversation |

End with the 1–2 highest-leverage improvements. Treat a gap the same way as a coding answer that wasn't optimal. Don't paste in a model design. Ask questions that lead them to the missing piece ("what happens to in-flight messages if that node dies?"), and let them revise `design.md`. A short sketch of what a strong answer would have covered comes last, and only for the parts they couldn't get to with hints.
