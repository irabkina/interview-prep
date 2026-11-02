# interview-prep

A [Claude Code](https://claude.com/claude-code) skill for technical interview prep in **coding/algorithms** and **system design**. It does two jobs:

- **Coach.** Reads a job description, works out what the role is likely to test, and builds a study plan that counts down to each interview stage. It teaches patterns before drilling them, schedules spaced reviews so topics don't go stale, and gives candid feedback.
- **Practice environment.** Sets up each problem as real files you open in your own IDE, with tests you can run. Options range from untimed drills to timed mock interviews where Claude plays the interviewer, plus redos that retest a skill you struggled with on a *new* problem.

All progress is saved as plain Markdown in your prep folder, so each session picks up where the last one stopped.

## Install

The skill keeps its state in the folder it runs in, so give it a dedicated folder and install it as a project skill there:

```bash
mkdir -p ~/interview-prep/.claude/skills
git clone https://github.com/irabkina/interview-prep.git ~/interview-prep/.claude/skills/interview-prep
```

You get this layout:

```
interview-prep/              ← run Claude Code here; your progress files go here too
└── .claude/skills/interview-prep/
    ├── SKILL.md
    ├── README.md
    └── references/
        ├── coding.md
        └── system-design.md
```

Don't install it in `~/.claude/skills/`. It would then load in every project and write its tracking files into whatever directory you happen to be working in.

## Start

```bash
cd ~/interview-prep
claude
```

Then type `/interview-prep`, or just say what you want. The skill triggers on its own when you paste a job description or ask for a practice problem, a mock or a review.

On the first run there's no history yet. It's worth telling Claude your preferred language, roughly how many hours a week you have, and what you already know well. That goes into `profile.md` and shapes everything that follows.

### Things to say

| You say | What happens |
|---|---|
| *(paste a job description or recruiter email)* | Adds the role and analyzes level, stack, likely rounds and topic weights. Then it asks about dates and format and builds a study plan. |
| "Give me a problem" | A **drill**: untimed, with a test file you run yourself. Hints only on request. |
| "Mock interview" / "Run a system design mock" | A **mock**: timed, with Claude in character as the interviewer. Ends with a scored debrief. |
| "Teach me sliding window" | A short lesson with a worked example, followed straight away by a drill. |
| "Review graphs" / "Quiz me" | A 5–10 minute recall check plus a spot-the-approach round. |
| "The onsite moved to Friday" / *(paste round feedback)* | Logs the update, revises the role analysis and re-plans from today. |
| "What should I do next?" / "How am I doing?" | The plan's next item, or a progress report per role against your dates. |
| "Let's continue" | Resumes an unfinished session from where it stopped. |

## How it works

**Plans scale to the time left.** With 7 days or less before a stage it runs in *triage* mode: no new topics, just reviews, redos and daily mocks. With 1–4 weeks it's *focused* on the role's highest-weighted topics. With months to go it covers everything, weighted by the job description.

**Practice modes**

| Mode | Timer | Claude's role | Tests |
|---|---|---|---|
| Drill | No | Coach at your side, hints on request | Visible, you run them |
| Mock | Yes, matched to the round | Interviewer in character | Examples only; hidden tests run afterward |
| Redo | Optional | Holds back hints and doesn't name the pattern | Visible, compared with your earlier attempt |

Timed online assessments (CodeSignal, HackerRank and similar) can be practiced as **solo mocks**, where Claude stays silent until you submit. Practical multi-part rounds ("parse these records… now add a tolerance… now explain the mismatches") reveal one part at a time, the way real interviewers do.

**Redos test the skill, not the problem.** If you needed hints, the skill is queued for a redo on a different problem that needs the same insight but looks different on the surface.

## Files it creates

All of these live in your prep folder, next to `.claude/`:

| File | Contents |
|---|---|
| `profile.md` | Language, level, weekly hours, active roles, unfinished sessions |
| `roles/<company>-<role>/role.md` | Job description, analysis, interview timeline, update log |
| `roles/<company>-<role>/plan.md` | The study plan, with a **Next up** line at the top |
| `sessions/YYYY-MM-DD-<slug>/` | Your work files, tests and `notes.md` for each session |
| `problems.md` | Every problem attempted, plus the redo queue |
| `topics.md` | Topics learned, with confidence and next review date |
| `weak-spots.md` | Things to work on, with evidence and status |
| `log.md` | One entry per session, newest first |

These files hold your job applications and practice history. Keep them out of the skill's repository. If you version the whole prep folder, keep it private.

## Requirements

- Claude Code
- A toolchain for your practice language. Tests use the language's usual framework: pytest for Python if it's installed in the project, otherwise `unittest`, so nothing extra is needed. JUnit, Jest and `go test` work for other languages.

## Scope

Covers coding/algorithms, practical coding rounds, timed assessments and system design. Behavioral rounds and multi-day take-home projects are tracked in the timeline so the plan leaves room for them, but the skill doesn't prepare you for them.

## License

MIT. See [LICENSE](LICENSE).
