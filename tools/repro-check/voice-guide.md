# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I'm a student developer helping out with bug triage and fixes. When I post on an issue, I keep it short and lead with exact terminal outputs, environment info, and repro steps. I don't waste maintainers' time with empty claims or speculation—just direct facts from local testing.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: name_evidence_first

State the exact command, error message, or environment details before giving any interpretation.

- Wrong: "I ran into the same issue on my setup and it looks like a parsing bug in the module."
- Right: "Confirmed on Python 3.11.4 / macOS 14.5. `pytest tests/test_parser.py` fails with `KeyError: 'config'`."

### Rule: state_reproduction_before_claiming

Only offer to work on an issue after reproducing it locally and attaching proof.

- Wrong: "I can take this! Let me know if I can work on it."
- Right: "Reproduced locally on Python 3.11 at commit `a1b2c3d`. I have a fix ready to open a PR for if this is still open."

### Rule: report_negative_results_without_apologies

If a bug doesn't reproduce, state your setup and test result cleanly without apologizing or guessing.

- Wrong: "Sorry, I tried to reproduce this but couldn't get it to fail, maybe I did something wrong?"
- Right: "Tested on Python 3.12 / Ubuntu 22.04 with `--verbose`. The test suite passed clean across 5 runs; log attached."

### Rule: cut_the_fluff

Skip corporate greetings and pleasantries; jump straight to the technical context.

- Wrong: "Hello maintainers! Hope you are having a great week! I took a look at this issue and..."
- Right: "Reproduced on `main`. Here's the stack trace:"

### Rule: disclose_ai_assistance_casually

When project guidelines ask for AI disclosure, state the tool used and what human verification you performed in one plain sentence.

- Wrong: "This comment and proposed code solution was generated using Claude 3.5 Sonnet."
- Right: "Used Claude to draft the repro steps; tested and verified the fix locally on Python 3.11."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Corporate email greetings ("Hello team!", "Hope you're having a great day!").
- Empty claim comments ("+1", "Any updates?", or "I can fix this" without local repro logs).
- Over-apologetic hedges ("Sorry if I'm wrong," "Apologies if this is a silly question").
- Vague promises without code or evidence ("I'll look into this tomorrow morning").
- Raw LLM output dumps or bot disclaimers ("As an AI assistant...").
- Claiming a bug is fixed without attaching diffs or test runner proof ("I fixed this locally, please close the issue").
- Presumptuous scope/priority claims ("This should be an easy 5-minute fix for the maintainers").
- Vague environment descriptions without explicit versions ("It failed on my Linux machine").
- Off-topic code style complaints in a bug thread ("Also this function should be refactored").
- Unsolicited architectural redesign proposals ("Instead of fixing this bug, we should rewrite the entire state module").
- Impatient pinging or maintainer badgering ("Why hasn't this been merged yet?", "Is anyone maintaining this project?").
- Unformatted walls of raw terminal logs directly in prose (use code fences or collapsible `<details>` tags).
