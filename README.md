# Chiluveru Snohith

**Full Stack Developer — B.Tech CSE '27 @ MRCET, Hyderabad**

[![GitHub](https://img.shields.io/badge/GitHub-Snohith-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Snohith)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-chiluveru--snohith-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/chiluveru-snohith)
[![Email](https://img.shields.io/badge/Email-chiluverusnohith%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:chiluverusnohith@gmail.com)

I build web apps with Next.js, React, and TypeScript — focused on real-time collaboration and data-backed product flows. Final-year CSE undergraduate looking for full-stack roles and internships.

---

## Skills

**Languages:** TypeScript, JavaScript, HTML, CSS, SQL, Java, Python (basic)
**Frontend:** React 19, Next.js 16 (App Router), Tailwind CSS, Framer Motion, Monaco Editor, Shadcn / Radix UI, React Hook Form + Zod, Leaflet / React-Leaflet
**Backend & real-time:** Node.js, REST / Server Actions, WebSockets (`ws`, `y-websocket`), Yjs CRDTs, Judge0 CE, Supabase (Auth, Postgres, SSR)
**Tooling:** Git, Vercel, Render, ESLint, `tsc --noEmit`

---

## Featured projects

### 1. Devlyst — real-time collaborative code workspace

Shared Monaco editing over Yjs: open a room, share the link, everyone types in the same files with live cursors. Run the current file through Judge0 and see stdout, exit code, and timing in the console panel.

- **Code:** https://github.com/Snohith/Devlyst
- **Live:** https://devlyst-web.onrender.com/
- **Stack:** Next.js 16, React 19, TypeScript, Yjs, `y-websocket`, Monaco Editor, Judge0 CE, Clerk (optional), Tailwind CSS

**What I built**

- Dedicated WebSocket relay (`server.js`) passing Yjs CRDT updates between clients in a room; file tree stored as a shared `Y.Map`, cursors and typing state on the awareness channel.
- Monaco integration with multi-file binding, Prettier formatting, Vim mode, language-aware extensions, and full-room ZIP export.
- Code execution via `POST /api/execute`: origin check, 20 runs/min per IP, 100 KB source cap, 5 s CPU / 128 MB limits on Judge0, with poll-and-timeout handling.
- Optional Clerk sign-in; without keys the app runs open with a `localStorage` display name. Two-service Render deploy (web + socket server). PWA installable.

**Run it**

```bash
git clone https://github.com/Snohith/Devlyst.git && cd Devlyst
npm install
node server.js          # terminal 1 — ws://localhost:1234
npm run dev             # terminal 2 — http://localhost:3000
```

**Known trade-offs (stated so they don't surface as surprises)**

- Rooms live in socket-server memory: when the last client leaves (or the process restarts), the room is gone. No database by design.
- Room access is the 5-digit room code — anyone with the link can join; not for sensitive code.
- Rate limiting is per-process memory (no shared Redis), and runs execute on the public Judge0 instance with its own quotas.

---

### 2. TravelMind — trip planner with budget-aware itineraries and maps

Enter origin, destination, dates, budget tier, and travel vibe; get a multi-day plan with daily timelines, costs in INR, food guides, and an interactive Leaflet map. Trips persist per user and are reloadable from the dashboard.

- **Code:** https://github.com/Snohith/TravelMind
- **Stack:** Next.js 16, React 19, TypeScript, Supabase (Auth, Postgres, SSR), Leaflet / React-Leaflet, React Hook Form + Zod, Tailwind CSS v4, Framer Motion

**What I built**

- Server Actions (`generateTrip`, `getTripById`, `getUserTrips`, `deleteTrip`) using the Supabase SSR server client; every read/write is scoped with `eq('user_id', user.id)` from the server session.
- Input validation with Zod, per-user/per-IP rate limiting, and a 50-trip per-user quota to bound database growth.
- Itinerary composer that reads the Supabase `cities` table with fallback to a local 10-destination knowledge base; duration and pricing adjust by budget tier (Budget / Standard / Luxury).
- Supabase Auth with single-session enforcement (`profiles.last_session_id`), paginated dashboard, and custom SVG Leaflet markers (no fragile default-icon patching).

**Run it**

```bash
git clone https://github.com/Snohith/TravelMind.git && cd TravelMind
npm install
# add NEXT_PUBLIC_SUPABASE_URL and NEXT_PUBLIC_SUPABASE_ANON_KEY to .env.local
npm run dev             # http://localhost:3000
```

**Known trade-offs**

- Generation is currently rule/template-based over curated data (~10 Indian destinations, extensible through the `cities` table) — not an LLM call. The shape is kept LLM-ready for a future edge-function swap.
- Day/activity inserts are sequential, not a single cross-table transaction; a mid-write failure can leave a partial trip.
- Rate limiting is in-memory (documented in code as demo-grade; Redis is the planned replacement). No `middleware.ts` route guard yet — protection lives in the client redirect plus the server-action session check.

---

## Education

**B.Tech, Computer Science & Engineering** — Malla Reddy College of Engineering and Technology (MRCET), Hyderabad — 2023–2027

## Contact

- Email: chiluverusnohith@gmail.com
- Phone: +91 8074278281
- LinkedIn: [linkedin.com/in/chiluveru-snohith](https://linkedin.com/in/chiluveru-snohith)
- GitHub: [github.com/Snohith](https://github.com/Snohith)
- Location: Hyderabad, India
