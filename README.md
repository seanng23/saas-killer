# SaaS Killer

Build your own version of an app you pay for, on your own computer, with your Claude subscription as the only AI cost.

I was paying about RM900 a year for Descript and using a small part of it. So I showed Claude how I used it, and within a day I had my own version doing those jobs. This is the skill I built to do it, cleaned up so you can use it.

## What you need

- A paid Claude plan and Claude Code. The Claude desktop app is enough to start.
- Your own account on the app you want to rebuild.

You don't need to be a developer. The skill checks for anything else it needs and walks you through installing it.

## Install

**Download:** get [saas-killer.zip](https://theaiosmethod.com/downloads/saas-killer.zip), then tell Claude Code "install the skill in Downloads/saas-killer.zip".

**One line, in Claude Code in a terminal:**

```
/plugin marketplace add seanng23/saas-killer
```

```
/plugin install saas-killer@saas-killer
```

**By hand:** copy `skills/saas-killer` into `~/.claude/skills/`.

## Use it

Open a new chat in Claude Code and say "build my own version of" and the app's name.

1. It asks what you use, what annoys you and which of your files the new version should read.
2. You log in to the app yourself, and it studies the screens you use. It never asks for your passwords.
3. It writes a plan in `SPEC.md` and writes no code until you say yes.
4. It builds your version on your computer and tests it with real data.
5. It hands it over with plain instructions and a list of what's left, so you can decide whether to cancel the app.

## Pick the right app

Good candidates are tools you use a small part of, on your own: a video editor, a transcriber, a content planner, a tracker or a report builder.

Leave these alone: anything that moves money, anything your customers log in to and anything that holds customer data you aren't set up to protect.

## Keep it clean

Rebuild what an app does for your own use. Never copy its name, logo, design, text, images or code, and check the app's terms before you study it. AI features use your Claude plan's usage.

More at [theaiosmethod.com/resources/app](https://theaiosmethod.com/resources/app).

## Licence

MIT
