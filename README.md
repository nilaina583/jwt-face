# Next.js UI Demo: Simulated Google/Face Auth + Todo

Frontend-only preview using Tailwind CSS and shadcn-style components. This simulates auth to validate the UI before wiring Google OAuth and Prisma.

## Stack

- Next.js App Router (14)
- Tailwind CSS + shadcn-style UI tokens/components
- LocalStorage for simulated session and todos

## Getting started

1. Install deps:
   - npm install
2. Run dev:
   - npm run dev

If you just review the code/design, no keys are required. Buttons simulate login and persist a user object in `localStorage`.

## Environment for Fullstack

Copy `.env.example` to `.env` and fill in values:

```
DATABASE_URL="postgres://USER:PASSWORD@HOST:PORT/DBNAME?sslmode=require"
NEXTAUTH_SECRET="generate_a_strong_random_string"
NEXTAUTH_URL="http://localhost:3000"

GOOGLE_CLIENT_ID="426592483557-0cvsro4q2ua9cektmh5egbjf114kvc1h.apps.googleusercontent.com"
GOOGLE_CLIENT_SECRET="your_google_client_secret"
```

Then run Prisma:

```
npx prisma generate
npx prisma migrate dev --name init
```

Routes added:
- `/api/auth/[...nextauth]` — NextAuth (Google, Prisma adapter)
- `/api/todos` — List/Create todos (requires session)
- `/api/todos/[id]` — Update/Delete todo (requires session)

Dashboard now tries the API first and falls back to `localStorage` if the API fails (e.g., missing DB/config during setup).

## What’s included

- `/` Landing page (marketing) with CTAs
- `/sign-up` Sign up: enter name and capture face (local avatar)
- `/auth` Login screen with simulated Google, Face login, and Demo login
- `/face-login` Webcam capture (no ML), produces a snapshot and “logs in”
- `/dashboard` Todo board scoped to current user, persisted in `localStorage`
- `/settings` Edit display name, link to face enrollment
- `/face-enroll` Capture and save face snapshot (local avatar)

## Tailwind + shadcn

- `tailwind.config.ts` exposes CSS variables as in shadcn/ui
- Lightweight UI primitives under `components/ui/*` (Button, Input, Card, Avatar)
- Ready to accept official shadcn components once packages are installed

Optional: add official shadcn components later

```
npx shadcn@latest init
npx shadcn@latest add button input card avatar
```

## Next steps (after UI validation)

1. Google OAuth: Integrate NextAuth/Auth.js with Google provider
2. Prisma: Add schema (User, Account, Session, Todo) and connect to your DB
3. Protect routes: Server-side session checks, middleware if needed
4. Face auth (real): Prefer WebAuthn/passkeys (biometric unlock) over custom face recognition. If you need facial recognition specifically, we can discuss on-device vs server inference and privacy safeguards.
# jwt-face
