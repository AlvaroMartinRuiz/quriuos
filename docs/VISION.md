# Quriuos — Vision & Roadmap

## What is Quriuos

Quriuos is a voice-AI platform that helps teenagers discover their interests,
talk with inspiring role models, and find their academic and professional
path — all through voice, in under 10 minutes.

Teenagers are going through a key stage where they're starting to figure out
what they like, what worries them, and what motivates them, but they often
lack a close, judgment-free space to express themselves. Knowledge feels
abstract and emotionally distant, and vocational decisions get made with
little real information — based on one-off tests rather than ongoing,
personal context.

Quriuos turns that around: instead of reading about a role model, the student
*talks* to a representation of them; instead of filling out a vocational test,
their profile evolves naturally out of real conversations.

---

## Vision

Accompany the student from their first sparks of curiosity all the way to
decisions about their future, building an emotional connection through voice
and turning curiosity into concrete vocational guidance.

Knowledge becomes interactive and emotional. The journey has three moments:

```
   Discover                Connect                   Guide
   ────────                ───────                    ─────
   listens and       →     fuels their         →     points toward
   motivates                curiosity                 academic/career paths
                          (role models)

   [ connection ]          [ curiosity ]            [ guidance ]
        \                       |                         /
         \                      |                        /
          ──────────  the student's evolving profile  ──────────
```

---

## How it works (technically)

Quriuos is **one continuous voice conversation**, not a multi-step form or a
set of separate tabs. A single orchestrator agent ("Quriuos") drives the
entire conversation and uses ElevenLabs' `transfer_to_agent` tool to hand off
to specialized agents based on what the student is talking about:

1. **Discover** — the orchestrator asks open-ended questions and detects real
   interests (sports, science, music, technology, art...).
2. **Connect** — once an interest is clear, it transfers to a character agent
   inspired by a real figure (e.g. Stephen Hawking for science, Steve Jobs or
   Elon Musk for technology, Cristiano Ronaldo or Messi for sports, Taylor
   Swift for music, Ibai Llanos for digital content), each running on an
   ElevenLabs voice clone with its own system prompt.
3. **Guide** — once enough context has built up across conversations, it
   transfers to the vocational-advisor agent, which uses the accumulated
   profile to suggest careers, academic areas, and professional paths.

All of this is built on a shared contract — a `StudentProfile` object
(interests, chats, vocational notes) persisted in `localStorage` — so every
agent reads and writes the same evolving profile, and the conversation can
resume naturally across sessions without repeating questions already
answered. There's no backend database for the hackathon prototype: agent
configuration lives in ElevenLabs, and student state lives on-device.

---

## Value proposition

A voice-AI platform that helps teenagers discover their interests, talk with
inspiring role models, and find their academic and professional path.

Built for an ElevenLabs hackathon, the project leans fully into ElevenLabs'
Conversational AI: inspirational voices, real-time conversation, custom
character voice clones, and an orchestrator that turns the whole experience
into a single flowing conversation instead of a menu of options.

---

## What's next — toward a fully-developed app

The hackathon build is a focused prototype of the full vision. Turning it
into a real product would mean tackling:

- **Real career/university data** — replacing the illustrative career
  suggestions with integration into real university and program catalogs.
- **Family & counselor dashboards** — giving parents and school counselors
  visibility into the student's evolving interests and recommendations (with
  the student's consent).
- **Accounts, parental controls & compliance** — a proper account system,
  parental consent flows, and full compliance with minors' data-protection
  requirements (the prototype intentionally avoids storing any data
  server-side).
- **A broader, curated character catalog** — going beyond the 7 launch
  characters to a wider, ongoing library of role models across more fields.
- **Smarter interest detection** — moving from prompt-driven detection during
  the conversation to a more robust signal-extraction layer, so the profile
  captures nuance even in shorter sessions.
- **Persistence beyond the device** — syncing the student profile to an
  account instead of `localStorage`, so progress isn't tied to a single
  browser/device.

The core idea stays the same at any scale: let a teenager's curiosity, voiced
out loud, be the thing that shapes their own academic and professional path.
