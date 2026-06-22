# ElevenLabs integration guide — Quriuos

This guide explains how to create the **conversational agents** in ElevenLabs
and connect them to the app. The app is already integrated with the
`@elevenlabs/react` SDK (`useConversation`): the visualizer reacts to real
voice audio, the transcript comes from real events, and the mute/end controls
actually work.

> **You already have the cloned VOICES.** What's left is to create one
> **Agent** per personality, assign its voice and prompt, and copy its
> `agent-id` into `.env.local`. Ready-to-paste prompts live in the `agentes/`
> folder.

---

## 1. Create each agent (step by step)

For each of the **9 agents** (Coach, Advisor, and 7 characters):

1. ElevenLabs dashboard → **Conversational AI → Agents → + New agent** (start blank).
2. **System prompt**: paste the contents of the *System prompt* section from
   the matching file in `agentes/` (e.g. `agentes/hawking.md`).
3. **First message**: paste the *First message* section from the same file.
4. **Voice**: select the **voice clone** you already have for that character.
5. **Language**: Spanish (or "auto") — the app's conversations are in Spanish.
6. **LLM**: a fast model for voice (e.g. GPT-4o mini or Gemini Flash).
7. **Save** and copy the **Agent ID** (shown in the agent's header, format
   `agent_xxxxxxxxxxxxxxxxxxxx`).

---

## 2. Public access (important for it to work without a backend)

The app connects from the browser using only the `agent-id`. For this to work
**without** standing up a token server:

- In each agent → **Security / Advanced** → enable
  **public / unauthenticated** access ("Enable authentication" = **OFF**, or
  "Allow public access").
- If there's a **domain allowlist**, add `http://localhost:3000` (development)
  and your deployment domain.

> If you'd rather keep the agents **private**, you need to generate a
> *conversation token* / *signed URL* on a backend using your API key and pass
> it to `startSession({ conversationToken })`. For the hackathon, **public was
> faster**.

---

## 3. Wiring the agent IDs into the app

1. Copy the example file:
   ```bash
   cd quriuos
   cp .env.local.example .env.local
   ```
2. Paste each `agent-id` into its variable:

   | Agent | Variable in `.env.local` | Voice to assign | Prompt |
   |---|---|---|---|
   | Personal coach | `NEXT_PUBLIC_EL_COACH_AGENT_ID` | warm/motivating voice | `agentes/coach.md` |
   | Vocational advisor | `NEXT_PUBLIC_EL_VOCATIONAL_AGENT_ID` | calm/trustworthy voice | `agentes/orientador.md` |
   | Stephen Hawking | `NEXT_PUBLIC_EL_HAWKING_AGENT_ID` | Hawking clone | `agentes/hawking.md` |
   | Steve Jobs | `NEXT_PUBLIC_EL_JOBS_AGENT_ID` | Jobs clone | `agentes/jobs.md` |
   | Elon Musk | `NEXT_PUBLIC_EL_MUSK_AGENT_ID` | Musk clone | `agentes/musk.md` |
   | Cristiano Ronaldo | `NEXT_PUBLIC_EL_CR7_AGENT_ID` | CR7 clone | `agentes/cr7.md` |
   | Lionel Messi | `NEXT_PUBLIC_EL_MESSI_AGENT_ID` | Messi clone | `agentes/messi.md` |
   | Taylor Swift | `NEXT_PUBLIC_EL_TAYLOR_AGENT_ID` | Taylor clone | `agentes/taylor.md` |
   | Ibai Llanos | `NEXT_PUBLIC_EL_IBAI_AGENT_ID` | Ibai clone | `agentes/ibai.md` |

3. **Restart** the dev server (`NEXT_PUBLIC_` variables are read at startup):
   ```bash
   npm run dev
   ```

---

## 4. Dynamic variables (student context)

The app sends context on every session via `dynamicVariables`. The prompts
already use them with `{{variable}}` syntax — ElevenLabs picks them up
automatically, no extra configuration needed.

| Variable | Used in | Content |
|---|---|---|
| `{{student_name}}` | all | the student's name |
| `{{interests}}` | all | list of detected interests |
| `{{character}}` | characters | name of the active character |
| `{{characters_talked}}` | advisor | role models the student has already talked to |
| `{{suggested_areas}}` | advisor | career areas suggested by the app |

> If a variable doesn't exist in your agent's prompt, ElevenLabs simply
> ignores it. You can reference only the ones you need.

---

## 5. Credit budget (~130k)

- Conversational AI consumes credits **per minute** of conversation.
- **Test in text mode first** inside the dashboard (uses no voice credits) to
  tune each prompt.
- Split ~30k per dev for development and **keep ~40k in reserve for the demo**.
- End the session (`End session`) after each test; don't leave it open.

---

## 6. Quick check

1. With at least the **Coach** agent configured, open the app at `/`.
2. Tap **Start talking** → grant the microphone permission.
3. You should see "Connecting…" → "Listening…/Speaking…", the visualizer
   moving with the real voice, and the transcript appearing.
4. If you see the *"Missing agent-id"* warning, check `.env.local` and restart.
5. If the connection fails, confirm the agent is **public** and the domain is
   on the allowlist.
