# `/straight-to-the-point`

> 🇧🇷 [Leia em português](./README.pt-BR.md)

Ever sent your boss a long message, only to get back *"ok, but what do you need from me?"*

The answer was in there. Buried in the fifth line, after the backstory, the
things you tried, and the "so, as you know...". Your reader stopped before
getting to it.

`/straight-to-the-point` is a [Claude Code](https://claude.com/claude-code)
skill that writes, rewrites and reviews work messages using **BLUF (Bottom
Line Up Front)**, the writing standard of the US Army: the request, the
decision or the conclusion goes in the first sentence. Context comes after,
only as much as the reader needs.

## The one test

> **If your reader stops after the first sentence, do they know what is
> happening and what they need to do?**

If not, the skill rewrites it until they do.

## Before and after

**Before** (the story in the order it happened):

```
Hey, so we started looking into the slowness on the premiums API yesterday,
checked the logs, tried a couple of things on the cache, and in the end found
a lock in the database that's making the query about 10x slower. We're fixing
it, but it'll take a day plus testing, so I think we'll need to push the
delivery a bit, if that's ok?
```

**After** (the bottom line first):

```
[APPROVAL] Move module X delivery to Thursday (Nov 16)

I need your approval to move the module X delivery from Tuesday to Thursday.

Why:
- We found a database lock that makes the premiums query ~10x slower.
- The fix is in progress and takes 1 day; the rest is testing.

If you'd rather keep Tuesday, I'll ship without the fix and open a card for
next sprint.
```

Same facts. The boss can answer the second one in five seconds, without
scrolling, and the alternative is already on the table.

## Why it exists

I'm a backend engineer heading toward software architecture. The further up
you go, the more of your job is writing for people with no time: status
updates, approval requests, incident reports, design proposals. A good
technical idea in a badly ordered message gets ignored.

I learned about BLUF from a short video about how senior engineers talk to
their managers, went looking for where it really came from, and turned what I
found into a skill I can call at the exact moment I'm about to hit send.

## What it does

The skill picks one of three modes from what you ask:

| Mode | You give it | You get back |
|---|---|---|
| **Write** | the situation, in any order | a ready-to-copy message |
| **Rewrite** | a draft you already wrote | the BLUF version of it |
| **Review** | a draft, asking for feedback | up to 3 points that break BLUF, plus the fix |

Under the hood it always follows the same six steps:

1. **Find the bottom line.** "If I could send only one sentence, which would it be?"
2. **Write it in 1–2 sentences:** what, who, by when, and why.
3. **Say what kind of answer you expect:** action, approval, or just reading.
4. **Context after, as short bullets.** No chronology, no effort log.
5. **Close with the next step:** who does what, and when.
6. **One subject per message.** Two subjects, two messages.

It ships with ready templates for the messages developers actually send:
approval request, status report, incident, help request (never just
*"hi, got a minute?"*), and technical proposal / ADR summary. Email subjects
get military-style tags (`[ACTION]`, `[APPROVAL]`, `[DECISION]`, `[INFO]`) so
the reader knows what the message wants from them before opening it.

## When it does *not* use pure BLUF

BLUF is not a universal rule, and the skill knows when to bend it:

- **Bad or sensitive news.** One short line to prepare the reader, then the
  fact, plainly. Opening with "the project failed" makes people stop reading
  in good faith.
- **The reader doesn't know the problem yet.** A conclusion without its
  problem makes no sense. State the problem in one sentence, then the answer.
- **Selling something new or controversial.** It switches to Barbara Minto's
  **SCQA**: Situation → Complication → Question → Answer.
- **You don't have a conclusion yet.** It won't invent one. "Root cause still
  unknown; next update at 3 PM" is a perfectly good bottom line.

## Installation

```bash
git clone https://github.com/VictorMarri/straight-to-the-point ~/.claude/skills/straight-to-the-point
```

On claude.ai, you can also upload the `SKILL.md` as a custom skill in your
settings.

## Usage

```
/straight-to-the-point I need to tell my manager the release slips 2 days because of a DB lock
```

```
/straight-to-the-point rewrite this: <paste your draft>
```

```
/straight-to-the-point review this email before I send it: <paste>
```

The skill answers in the language you write in. Its instructions are in
Portuguese, the rules are not.

## Where it comes from

- **US Army Regulation 25-50**, *Preparing and Managing Correspondence*: the
  two essential rules of Army writing are bottom line up front and active
  voice.
- **DA Pamphlet 600-67**, *Effective Writing for Army Leaders* (1986): start
  with the information you would keep if you had to throw the rest away.
- **Kabir Sehgal**, *How to Write Email with Military Precision*, Harvard
  Business Review (2016): subject-line keywords and BLUF for civilian email.
- **Barbara Minto**, *The Pyramid Principle*: SCQA and how to organize
  everything under the main point.
- **Bryan Garner** (ABA Journal): the critique that BLUF needs the problem to
  be clear first, which shaped the "when not to use" section.

## License

[MIT](./LICENSE)
