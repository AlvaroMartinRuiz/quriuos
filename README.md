# Quriuos

> Plataforma de voz con IA que ayuda a adolescentes a descubrir sus intereses, conversar con referentes inspiradores y encontrar su camino académico y profesional.

Proyecto desarrollado en un hackathon organizado por **ElevenLabs**, en equipo con [Mateo Sinelnik](https://github.com/Ramputink) y Fernando. [Repo original del equipo](https://github.com/Ramputink/hackatonEvolve).

---

## Qué es Quriuos

Quriuos es **una sola conversación de voz continua**, sin menús ni pestañas: el estudiante habla con "Quriuos", un agente orquestador que detecta sus intereses y transfiere automáticamente la charla, según el tema, a uno de varios agentes especializados ([ElevenLabs Conversational AI](https://elevenlabs.io/conversational-ai) + `transfer_to_agent`):

1. **Descubrir** — Quriuos escucha al estudiante y detecta intereses reales (deporte, ciencia, música, tecnología...) con preguntas abiertas.
2. **Conectar** — en cuanto detecta un interés claro, transfiere la conversación a un referente inspirado en una figura real (Hawking, Jobs, Musk, CR7, Messi, Taylor Swift, Ibai) clonado con voz de ElevenLabs.
3. **Orientar** — con suficiente contexto acumulado, transfiere al orientador vocacional, que sugiere carreras y áreas académicas a partir de todo el perfil.

Cada interés y cada chat se guardan en un perfil evolutivo (`localStorage`) con memoria persistente entre sesiones, visible en el drawer "Mi futuro". En lugar de leer sobre un referente, el estudiante *habla* con una representación de él; en lugar de rellenar un test vocacional, su perfil evoluciona de forma natural a partir de cada conversación.

---

## Stack tecnológico

- **Next.js 16** (App Router) — framework
- **TypeScript** — tipado
- **Tailwind CSS v3** — estilos con design tokens propios
- **ElevenLabs Conversational AI** — agentes de voz en tiempo real (`@elevenlabs/react`)
- **localStorage** — perfil del estudiante persistido en el dispositivo, sin servidor

---

## Empezar en local

```bash
git clone https://github.com/AlvaroMartinRuiz/quriuos.git
cd quriuos

npm install

cp .env.local.example .env.local
# Edita .env.local con tu API key y agent-ids de ElevenLabs

npm run dev
```

Abre [http://localhost:3000](http://localhost:3000) en el navegador.

### Configurar los agentes de ElevenLabs

Cada bloque/personaje necesita su propio agente conversacional creado en el [dashboard de ElevenLabs](https://elevenlabs.io/app/conversational-ai/agents). Los pasos detallados están en [docs/GUIA_ELEVENLABS.md](docs/GUIA_ELEVENLABS.md); también puedes automatizar la creación con:

```bash
node scripts/create-agents.mjs
```

> La API key de ElevenLabs nunca debe ir al repo: solo vive en tu `.env.local`, que está en `.gitignore`.

---

## Estructura del proyecto

```
app/
  page.tsx            # Pantalla única: chat con Quriuos + drawer "Mi futuro"
  api/elevenlabs-token/  # Endpoint server-side para tokens de conversación
components/           # VoiceSession (widget de voz), ProfileSummary, ParticleField...
lib/                  # profile.ts (contrato StudentProfile), characters.ts, careers.ts, elevenlabs.ts
agentes/              # Prompts de sistema de cada agente (orquestador, personajes, orientador)
scripts/              # Automatización de creación/configuración de agentes en ElevenLabs
docs/                 # Documentación del proyecto (ver abajo)
```

---

## Documentación adicional

- [docs/PROYECTO.md](docs/PROYECTO.md) — visión y propuesta de valor completa
- [docs/PRD.md](docs/PRD.md) — documento de requisitos de producto
- [docs/TEAM_PLAN.md](docs/TEAM_PLAN.md) — plan de reparto de trabajo durante el hackathon
- [docs/GUIA_ELEVENLABS.md](docs/GUIA_ELEVENLABS.md) — guía paso a paso para configurar los agentes
- [docs/GUION_DEMO.md](docs/GUION_DEMO.md) — guion usado para la demo del hackathon

---

## Créditos

Hecho en equipo con [Mateo Sinelnik](https://github.com/Ramputink) y Fernando durante un hackathon de ElevenLabs.
