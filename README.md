# Gemini Chat App

A real-time 1:1 chat app with a built-in **Gemini AI assistant**. Sign in with Google, message people live over WebSockets, and ping the AI whenever you need it.

![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-4-06B6D4?logo=tailwindcss&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?logo=prisma&logoColor=white)
![Postgres](https://img.shields.io/badge/Postgres-Supabase-4169E1?logo=postgresql&logoColor=white)
![Socket.io](https://img.shields.io/badge/Socket.io-4-010101?logo=socketdotio&logoColor=white)
![NextAuth](https://img.shields.io/badge/NextAuth-v5-EB5424)
![Gemini](https://img.shields.io/badge/Gemini-API-8E75B2?logo=googlegemini&logoColor=white)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?logo=vercel&logoColor=white)

## What's in it

- Google sign-in via NextAuth v5 with the Prisma adapter
- Live 1:1 messaging over Socket.io (no polling)
- Online / offline presence and "last seen" timestamps
- Chat history persisted in Postgres
- AI chat tab powered by the Gemini API, with a per-user credit counter
- Image messages and emoji picker
- Voice recording UI, shimmer loaders, auto-scroll to latest
- Fully responsive: desktop sidebar, mobile bottom nav

## Stack

| Layer | Tools |
| --- | --- |
| Frontend | Next.js 16 App Router, React 19, TypeScript |
| UI | Tailwind v4, Radix UI primitives, shadcn-style components, Framer Motion, Lucide |
| Auth | NextAuth v5 (Google provider) |
| Database | Postgres on Supabase, Prisma 5 |
| Realtime | Socket.io 4 (server + client) |
| AI | Google Gemini API |
| Hosting | Vercel |

## Running it locally

```bash
git clone https://github.com/taiayman/gemini-chat-app.git
cd gemini-chat-app
npm install
```

Create a `.env` with:

```env
DATABASE_URL=postgresql://...
DIRECT_URL=postgresql://...
NEXTAUTH_SECRET=...
NEXTAUTH_URL=http://localhost:3000
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
GEMINI_API_KEY=...
```

Then:

```bash
npx prisma migrate dev
npm run dev
```

Open http://localhost:3000.

## Project layout

```
src/
  app/
    api/          # NextAuth + chat + AI route handlers
    chat/         # 1:1 conversation UI
    ai/           # Gemini assistant tab
    login/        # Google sign-in page
  components/ui/  # Radix + Tailwind UI primitives
  hooks/          # Socket + presence hooks
  lib/            # Prisma client, helpers
prisma/schema.prisma
```

## Notes

The `User` model carries a `credits` field that gets decremented on each AI call, so it's an easy hook for billing or a free-tier limit later. Message reads are tracked with `isRead`, which means unread badges work without an extra table.
