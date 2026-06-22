# Quriuos

> A voice-AI platform that helps teenagers discover their interests, talk with inspiring role models, and find their academic and professional path.

Built during a hackathon organized by **ElevenLabs**, together with [Mateo Sinelnik](https://github.com/Ramputink) and [Fernando S. Cardo](https://www.ferscardo.com/).

---

## What is Quriuos

Quriuos is **one continuous voice conversation** — no menus, no tabs. The student talks to "Quriuos," an orchestrator agent that detects their interests and automatically transfers the conversation, based on topic, to one of several specialized agents ([ElevenLabs Conversational AI](https://elevenlabs.io/conversational-ai) + `transfer_to_agent`):

1. **Discover** — Quriuos listens to the student and detects real interests (sports, science, music, technology...) through open-ended questions.
2. **Connect** — once a clear interest is detected, it transfers the conversation to a character inspired by a real figure (Hawking, Jobs, Musk, CR7, Messi, Taylor Swift, Ibai), voice-cloned via ElevenLabs.
3. **Guide** — once enough context has been gathered, it transfers to the vocational advisor, who suggests careers and academic areas based on the full profile.

Every interest and chat is saved to an evolving profile (`localStorage`) with memory that persists across sessions, visible in the "My future" drawer. Instead of reading about a role model, the student *talks* to a representation of them; instead of filling out a vocational test, their profile evolves naturally from each conversation.

---

## Tech stack

- **Next.js 16** (App Router) — framework
- **TypeScript** — typing
- **Tailwind CSS v3** — styling with custom design tokens
- **ElevenLabs Conversational AI** — real-time voice agents (`@elevenlabs/react`)
- **localStorage** — student profile persisted on-device, no server

---

## Getting started locally

```bash
git clone https://github.com/AlvaroMartinRuiz/quriuos.git
cd quriuos

npm install

cp .env.local.example .env.local
# Edit .env.local with your ElevenLabs API key and agent IDs

npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Setting up the ElevenLabs agents

Each block/character needs its own conversational agent created in the [ElevenLabs dashboard](https://elevenlabs.io/app/conversational-ai/agents). Detailed steps are in [docs/GUIA_ELEVENLABS.md](docs/GUIA_ELEVENLABS.md); you can also automate creation with:

```bash
node scripts/create-agents.mjs
```

> The ElevenLabs API key must never go into the repo: it only lives in your `.env.local`, which is in `.gitignore`.

---

## Project structure

```
app/
  page.tsx            # Single screen: chat with Quriuos + "My future" drawer
  api/elevenlabs-token/  # Server-side endpoint for conversation tokens
components/           # VoiceSession (voice widget), ProfileSummary, ParticleField...
lib/                  # profile.ts (StudentProfile contract), characters.ts, careers.ts, elevenlabs.ts
agentes/              # System prompts for each agent (orchestrator, characters, advisor)
scripts/              # Automation for creating/configuring agents in ElevenLabs
docs/                 # Project documentation
```

---

## Credits

Built as a team with [Mateo Sinelnik](https://github.com/Ramputink) and [Fernando S. Cardo](https://www.ferscardo.com/) during an ElevenLabs hackathon.
