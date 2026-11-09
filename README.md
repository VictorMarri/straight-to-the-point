# `/straight-to-the-point`

> 🇧🇷 [Leia em português](./README.pt-BR.md)

A [Claude Code](https://claude.com/claude-code) skill that writes, rewrites and
reviews work messages using **BLUF (Bottom Line Up Front)**, the US Army writing
standard: the request, decision or conclusion goes in the first sentence.

## Before and after

**Before:**

```
Hey, so we started looking into the slowness on the premiums API yesterday,
checked the logs, tried a couple of things on the cache, and found a DB lock
that makes the query ~10x slower. The fix takes a day plus testing, so I think
we'll need to push the delivery a bit, if that's ok?
```

**After:**

```
[APPROVAL] Move module X delivery to Thursday (Nov 16)

I need your approval to move the module X delivery from Tuesday to Thursday.

Why:
- A DB lock makes the premiums query ~10x slower.
- The fix takes 1 day; the rest is testing.

If you'd rather keep Tuesday, I'll ship without the fix.
```

## Installation

```bash
git clone https://github.com/VictorMarri/straight-to-the-point ~/.claude/skills/straight-to-the-point
```

## Usage

```
/straight-to-the-point tell my manager the release slips 2 days because of a DB lock
/straight-to-the-point rewrite this: <draft>
/straight-to-the-point review this email: <draft>
```

The skill answers in the language you write in.

## Sources

US Army AR 25-50 and DA PAM 600-67 · Kabir Sehgal, HBR (2016) · Barbara Minto, *The Pyramid Principle*

## License

[MIT](./LICENSE)
