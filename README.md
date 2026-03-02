# Technical Competence Router

AI-powered support routing that assesses a caller's technical competence in real-time and routes them to the right support tier.

## How It Works

```
Phone Lookup → IVR → Competence Assessment → Tier Routing
```

1. **Phone lookup** — Returning customers are recognized and routed directly based on their previous assessment
2. **IVR** — New callers describe their problem and what they've already tried
3. **Categorization** — The LLM classifies the caller as technical or non-technical based on the conversation
4. **Routing** — Callers land with the right agent:
   - **L1 (Jim)** — Friendly, walks through basics one step at a time (restart, check cables, clear cache)
   - **L2 (Kat)** — Direct and efficient, dives into logs, configs, and diagnostics

## Features

- **Chat support** (`/`) — Text-based support flow with the full routing pipeline
- **Voice support** (`/voice`) — Real-time voice calls via OpenAI Realtime API + WebRTC, with distinct voice profiles per tier
- **Returning customer recognition** — Phone number lookup skips IVR for known callers
- **Database viewer** (`/users`) — Browse stored users and their competence ratings

## Tech Stack

- **Framework**: Next.js (App Router), React, TypeScript
- **Styling**: Tailwind CSS
- **AI**: OpenAI GPT-4o-mini (chat), OpenAI Realtime API (voice)
- **Database**: Neon PostgreSQL (serverless)

## Getting Started

### Environment Variables

Create a `.env.local` with:

```
OPENAI_API_KEY=your-openai-key
DATABASE_URL=your-neon-postgres-connection-string
```

### Run

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Project Structure

```
app/
├── api/
│   ├── chat/route.ts          # Chat completion + routing logic
│   ├── lookup/route.ts        # Phone number database lookup
│   └── voice/session/route.ts # Voice session token creation
├── components/
│   ├── ChatWindow.tsx         # Message display UI
│   ├── PhoneInput.tsx         # Phone number entry
│   ├── SupportChat.tsx        # Chat flow orchestrator
│   └── VoiceSupport.tsx       # WebRTC voice client
├── lib/
│   ├── agents.ts              # System prompts for IVR, L1, L2
│   ├── voice-agents.ts        # Voice-specific prompts + tools
│   ├── openai.ts              # OpenAI client
│   └── types.ts               # TypeScript interfaces
├── page.tsx                   # Chat support page
├── voice/page.tsx             # Voice support page
├── users/page.tsx             # Database viewer
└── db.ts                      # Neon database client
```
