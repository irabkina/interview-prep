# Coding

## Choosing problems
Use problems that resemble well-known interview questions, but state them in your own words with a little framing, the way an interviewer would. Vary the difficulty to match the role's level and recent results in `problems.md`. If they solved the last two cleanly, step up a level. Never repeat a problem from the attempts table, and that includes redos, which use a new problem that needs the same skill (see "Redos and the practice index" in SKILL.md). Record the precise skill each problem tests, since that's what redos and reviews key on.

Topic coverage for plans and lessons:
- Arrays & hashing, two pointers, sliding window
- Stacks / monotonic stack, queues
- Binary search, including searching over an answer space
- Linked lists
- Trees: traversal, BST, LCA, serialization
- Heaps / top-k / merging streams
- Graphs: BFS/DFS, topological sort, union-find, shortest paths
- Backtracking
- Dynamic programming: 1D, 2D, knapsack-style, intervals
- Intervals, greedy
- Tries, bit manipulation (lower priority)

Use the language from `profile.md`, or the one the role's format details require.

## Practical rounds

Many companies skip LeetCode-style problems in favor of tasks that look like the actual job: parsing, transforming, validating, matching or aggregating records, or building a small class with an API. If the role's format details point that way, use these instead of puzzles, set in the role's domain.

- **Build the problem in parts.** Part 1 is straightforward. Each later part adds a requirement that changes the earlier code ("now allow a date tolerance", "now report why each record didn't match"). Reveal one part at a time, the way interviewers do. How well part 1's code holds up when part 2 arrives is the real test.
- **Reveal each new part in the `solution.py` docstring**, not in a separate file, so the whole problem stays in one place, the way an interview tool shows it. Add the part to the end of the top docstring under a divider (`Part 2 of 3 — <title>`), and title the first part `Part 1 of N` from the start. Add new tests in a new file (`test_part2.py`, …), so the earlier tests keep checking that nothing broke. Editing the docstring between parts is the one exception to "the solution file belongs to the user". Touch only the docstring, never their code, and only once they've finished the previous part. "Finished" means its tests pass (in a mock, the hidden tests for that part, run once they say they're done) and you've wrapped it up. Then ask which mode the next part should start in (see "Multi-part problems" in SKILL.md), and only then append it.
- **Modes are per part.** Record each part's mode, any mid-part switch and the hints given in `notes.md`. A mock debrief scores only the parts and stretches that ran as a mock. Never write later parts in advance, preview them, or describe what's coming, because finding out the new requirement only when it arrives is part of the exercise.
- **The algorithms are easy, so the bar moves.** Judge code structure and naming, types, edge cases in messy realistic data, choosing standard-library tools well (`defaultdict`, `Counter`, `dataclasses`, `sorted(key=…)`), speed, and how cleanly the code takes the next requirement.
- **Leave real ambiguity in the data.** Duplicates, missing fields, off-by-one dates, negative amounts. Spotting them and asking about them, or writing down an assumption, is what a senior engineer does.
- Score with the same rubric, but read "problem solving" as handling requirements and edge cases rather than finding an optimal algorithm.

## Session files

The user codes in a real file in their own IDE, so they practice with their usual editor and keyboard. Coding in chat would feel nothing like an interview. In `sessions/YYYY-MM-DD-<slug>/`:

- **`solution.<ext>`** (using the language's usual extension):
  - **The problem statement** as a comment or docstring at the top, the way it would appear in an interview tool, with examples. In a mock, leave the constraints as vague as you plan to state them, because clarifying them is part of the exercise. In a drill, state them fully.
  - **A stub:** the function or class signature, with an empty body for the user to fill in.
  - **A runner for the given examples**, such as an `if __name__ == "__main__":` block or a `main` that prints the expected and actual results.
- **`test_solution.<ext>`**, in drills and redos only: a fuller test suite the user can run themselves, in the language's usual test framework (pytest, JUnit, Jest, `go test`…; for Python, check `profile.md` for the project's environment and use pytest if it's there, otherwise `unittest`, so nothing needs installing), covering edge cases (empty input, a single item, duplicates, large inputs, overflow). Running it themselves is part of the practice. They see a failure, figure out why, and fix it. Tell them the command to run it.
- **`notes.md`**: the mode, the problem, highlights and feedback.

In a mock, the edge-case tests stay hidden, because a real interviewer doesn't hand them out. Keep them in a separate script and run it only after the user says they're done. If the role's format details say code won't be run (a shared doc or whiteboard style), leave out the runner and tell the user to solve it without executing anything. Treat it as a dry run.

Once the files are set up, give the user the full path to open.

## Working alongside the user

- **The solution file belongs to the user.** Don't edit it while they're working. In a mock, that's because interviewers don't type into the candidate's editor. In a drill, it's because writing the code themselves is the whole point. If you want to show an idea in code, write a small separate snippet in chat or in `notes.md`, never their solution. There are two exceptions: appending the next part to the docstring, and swapping in a part's solution when they choose "get the solution and move on" and say yes to the swap.
- **Re-read the file every time they message you**, like someone watching a shared screen, so your questions and hints reflect where their code is right now. If you can't tell what changed, ask them to walk you through it instead of guessing.
- In a mock, run the code only if they ask or the format allows it, and report the output the way an interview tool would. In a drill, encourage them to run their tests themselves, and run them yourself only if they ask.

## During a mock
- If they start coding without asking anything, let them. Noting that is part of the debrief.
- When they say they're done, ask them to walk through a test case by hand before you reveal any bugs. Catching their own bugs is the skill being tested. Then run the hidden tests without modifying their file.
- Ask for time and space complexity if they don't offer it.
- Tell them the time at natural checkpoints ("about 15 minutes left").
- Default: 45 minutes, one medium problem, plus a follow-up if time allows. Use the round format in the role's `role.md` when it's known (a phone screen is often 30 minutes with an easy or medium problem).

## During a drill
- If they ask, discuss the approach before they code. In a drill, thinking out loud with a coach is the right way to work.
- When they run the tests and ask nothing else, report the result (pass count, failing test names) and stop. When they're stuck, ask what the failing case shows before you point at the bug. Don't pre-empt bugs you can see but they haven't hit yet. The tests will surface them.
- Once it passes, ask about complexity and whether there's a better approach. If there is one, run the follow-up below.
- After the set, sum up the pattern in one or two lines. It goes in `notes.md`.

## Getting to the optimal solution

If an attempt didn't reach the optimal solution, don't hand it over. Working it out themselves with a little help sticks far better than reading an answer, and the insight they arrive at is the part that transfers to the next problem. After a mock this is an untimed follow-up. In a drill, it's simply the next step.

1. After a mock, copy their file to `solution-2.<ext>`, so the timed attempt is preserved as the record and they keep working in the copy. In a drill, they can keep editing the same file.
2. Start from their own approach, not from the answer. Ask what dominates the running time, or where the work gets repeated. Often they can see the problem in their own code once someone points them at it.
3. Hint step by step. Ask a nudging question, then name the technique or data structure, then give one concrete step. Give the next hint only after they've tried with the current one.
4. Once they get there, confirm it with the tests and a quick complexity check. Point out the general pattern they just used ("when you're re-scanning a window, think sliding window"), since that's what will help them recognize it next time.

Write out a reference solution in `reference.<ext>` only if they ask for it, or if they're still stuck after the most concrete hint. Even then, explain the key insight first, and keep it separate from their files. Record how they got there in `problems.md`, because it determines the redo schedule.

## Mock debrief rubric (score 1–4 each)
| Dimension | 4 looks like |
|---|---|
| Problem solving | Clarified constraints, considered more than one approach, reached the optimal one with at most a small nudge |
| Code | Correct, readable, idiomatic. Sensible names, no tangled control flow |
| Communication | Narrated their reasoning and tradeoffs without being prompted, easy to follow |
| Testing | Traced examples, found their own bugs, covered edge cases (empty, single item, duplicates, overflow) |

Also report: whether it was solved (yes/partial/no), whether it was optimal, the time used and the hints given (and at what level). End with the 1–2 most important things to change. If they didn't reach the optimal solution, say so, without revealing it, and offer the follow-up. The follow-up doesn't change the scores, which reflect the timed attempt.

Hiring-bar shorthand you can give: mostly 4s with few hints = strong hire signal. Mixed 3s = borderline. Any 1, or not solved without heavy hints = likely no-hire for that round.
