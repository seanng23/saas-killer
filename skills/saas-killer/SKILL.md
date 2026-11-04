---
name: saas-killer
description: Studies an app the user pays for while they're logged in, then builds their own version on their computer, with their Claude subscription as the only AI cost. Use when the user says "saas killer", "build my own version of [app]", "clone this app", "study this app and build our own" or sends an app's link and says they want their own.
---

# SaaS Killer

Turn an app I pay for into my own version: its logic, my data, my way of
working and my Claude subscription as the only AI cost. A general app has to
serve thousands of customers and my version only has to serve me, so build it
around my own files and data.

## Rules that apply every time

1. Never touch my passwords. I log in to the app myself. Never ask for, see,
   type or save a password. If you reach a login page, stop and say "log in,
   then tell me you're in."
2. Study only an app I have my own account on, and only the screens my account
   can open.
3. Rebuild what the app does, never what it looks like. Don't copy its name,
   logo, design, text, images or code. My version gets its own plain name and
   its own simple design.
4. Use no paid API keys in the app you build. AI features run on my Claude
   subscription (see Step 3). Data comes from my own files, my exports from the
   app or free public sources, and free tools may run on my computer. If a
   feature has no free source, flag it in the spec and let me decide. Never add
   a paid service without asking.
5. Keep it on my computer: run it on 127.0.0.1 only, don't put it online and
   don't add accounts or logins to it.
6. Treat SPEC.md as a contract. Read it before every build step and add nothing
   that isn't in it.
7. Explain everything in plain English. I'm not a developer.
8. If the app moves money, has customers logging in or holds customer data,
   stop and tell me to keep paying for it.

## Step 1: Ask

Ask me these in one message:
- The app's link and what I pay for it.
- Which parts of the app I use, and how often. Push me to cut: a small version
  I use every week beats a full copy I never open.
- What annoys me about it, and what I wish it did.
- What should make this version mine: which of my files, data or brand notes it
  should read.

Then open the app in a browser you can read, such as the Browser pane in the
Claude desktop app. Wait for me to log in and tell you I'm in. If you have no
browser tool, tell me and work from screenshots and text I paste instead.

## Step 2: Study

Go through every screen I use, one at a time.

- Read the page text first and use screenshots for layout only. Screenshots can
  show images as black, and the text stays reliable.
- If you can't open a page, ask me to click through to it.
- For each screen, write down what it shows, what data it needs, what I do on
  it, where AI does the work and what's generic about it. The generic part is where my version can beat
  the app.

Create a folder for the app at ~/Code/[app-name] and save this there as
teardown.md, with one line per feature on what my version does
better. Show it to me, then help me cut the list to the smallest version I'd
use every week. Everything else goes under "Later".

## Step 3: Spec (stop here for my yes)

Write SPEC.md in the app's folder. Default to Next.js,
TypeScript, Tailwind and SQLite (better-sqlite3), with a small Python script if
data has to be pulled in. Change this only if you tell me why. The spec covers:

- The features, the pages and the database tables.
- The port it runs on: pick an unused one in the 30xx range.
- How data gets in. Data pulls fill the database and pages read from the
  database, so opening a page never fetches anything.
- How AI features work. Each one calls Claude Code in the background:
  claude -p --output-format json --model [model]. Remove CLAUDECODE,
  CLAUDE_CODE_ENTRYPOINT and ANTHROPIC_API_KEY from the environment of that
  call, so it can't bill outside my subscription. Use the strongest
  model for judgment work and a cheaper one for mechanical work, and let me
  change the model from a settings page. Tell me these calls use my Claude
  plan's usage.
- What AI features know. Every prompt includes real rows from the database and
  a short profile file about me or my business. Every prompt also carries this
  rule: never invent facts, and show a missing number as [N].

Show me the spec as a numbered plan in plain English, with a check for each
step. Stop. Write no code until I say yes.

## Step 4: Build

Before you build, check Node and Python are installed and walk me through
installing anything missing. Build the foundation first, then the features, then the polish. If several
agents build at once, run the builds one at a time, because they share one
build folder and collide.

Test it yourself before you show me: load real data, run every AI feature once
and read what it wrote. A success message doesn't count as a test. Fix what
breaks, then walk me through it one feature at a time.

### Known traps

- AI calls from the app log in separately from the desktop app. They return
  "Not logged in" until I run claude /login in a terminal. Check this at the
  start of the build. First check that the claude command exists, and if it
  doesn't, walk me through installing Claude Code for the terminal.
- Fast repeat requests to a website fail with errors that look like code bugs.
  Space them 60 to 90 seconds apart and retry failures after 10 minutes.
- If you use yt-dlp, it rejects ytsearchdate. Use ytsearch, fetch 3 times as
  many results and filter the dates in Python.
- AI features invent credentials and facts about me. Put the never-invent rule
  in the first prompt.

## Step 5: Hand over

1. Add the app to .claude/launch.json with its name, command and port, so I can
   start it from Claude.
2. Write a one-page README in plain English: how to start it, where my files
   live, how to back them up and what to ask you when something breaks.
3. List what's still under "Later", so I can decide whether to cancel the app.
4. Offer a nightly data pull once the data settles. Don't add it without my yes.
