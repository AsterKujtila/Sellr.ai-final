# SELLR.ai — AI Sales Coach for Whop Sellers

> Built with Next.js 14 · Supabase Auth · Anthropic Claude · Tailwind CSS  
> UI/UX architecture identical to MindCore — glassmorphism, mobile-first, phone-frame desktop.

---

## Stack

| Layer     | Tech                              |
|-----------|-----------------------------------|
| Framework | Next.js 14 (App Router)           |
| Auth      | Supabase Google OAuth (PKCE)      |
| Database  | Supabase PostgreSQL + RLS         |
| AI        | Anthropic Claude claude-opus-4-5  |
| Fonts     | Figtree (sans) + Fraunces (serif) |
| Styling   | Tailwind CSS 3 + glassmorphism    |
| Hosting   | Vercel                            |

---

## Features

- ✅ Google OAuth (server-side PKCE — same as MindCore)
- ✅ Mobile-first with desktop phone-frame (430px max-width)
- ✅ 4 tabs: **Chat** · **Offers** · **Store** · **Credits**
- ✅ AI Chat with voice input + TTS read-aloud
- ✅ Offer Builder (headline, bullets, CTA, trust line)
- ✅ Store Analyzer (score, revenue leaks, quick wins)
- ✅ Credits system with plan tiers
- ✅ Settings bottom sheet with drag-to-dismiss gesture
- ✅ Account management + feedback form
- ✅ Auth guard + auto profile creation
- ✅ Row Level Security on all tables
- ✅ Vercel-ready with `vercel.json`

---

## Deploy in 4 Steps

### 1. Push to GitHub

```bash
git init && git add . && git commit -m "init: SELLR.ai"
git remote add origin https://github.com/YOUR_USER/sellr-ai.git
git push -u origin main
```

### 2. Supabase setup

1. Create project at [supabase.com](https://supabase.com)
2. **SQL Editor** → paste + run `supabase/migrations/001_schema.sql`
3. **Authentication → Providers → Google → Enable**
   - Add your Google OAuth Client ID + Secret
4. **Authentication → URL Configuration → Redirect URLs**, add:
   ```
   https://YOUR_APP.vercel.app/auth/callback
   http://localhost:3000/auth/callback
   ```

### 3. Vercel deploy

1. [vercel.com/new](https://vercel.com/new) → Import GitHub repo
2. Add environment variables:

```
NEXT_PUBLIC_SUPABASE_URL       = https://xxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY  = eyJ...
ANTHROPIC_API_KEY              = sk-ant-api03-...
```

3. **Deploy**

### 4. Google Cloud Console

In your OAuth client → **Authorized redirect URIs**, add:
```
https://YOUR_SUPABASE_PROJECT.supabase.co/auth/v1/callback
```

---

## Local Development

```bash
npm install
cp .env.example .env.local
# Fill in the 3 env vars
npm run dev
# → http://localhost:3000
```

---

## Project Structure

```
sellr-ai/
├── app/
│   ├── layout.tsx                  # Root layout (Figtree + Fraunces fonts)
│   ├── globals.css                 # Design system + Tailwind
│   ├── page.tsx                    # Root redirect
│   ├── login/page.tsx              # Google OAuth login
│   ├── chat/page.tsx               # Main shell (all 4 tabs)
│   ├── auth/callback/route.ts      # PKCE token exchange
│   └── api/
│       ├── auth/google/route.ts    # PKCE OAuth initiator
│       ├── chat/route.ts           # Claude AI proxy
│       ├── offers/route.ts         # Offer copy generator
│       ├── store/route.ts          # Store analyzer
│       ├── feedback/route.ts       # Feedback submissions
│       └── account/delete/route.ts # Account deletion
├── components/
│   ├── ui/                         # Radix-based UI primitives
│   ├── app-logo.tsx                # SELLR logo mark
│   ├── auth-guard.tsx              # Client-side auth check
│   ├── bottom-navigation.tsx       # 4-tab nav bar
│   ├── chat-view.tsx               # AI chat with voice
│   ├── credits-view.tsx            # Credits + plan management
│   ├── desktop-shell.tsx           # Phone frame wrapper
│   ├── menu-icon.tsx               # Hamburger icon
│   ├── offers-view.tsx             # Offer copy builder
│   ├── page-header.tsx             # Page top header
│   ├── settings-menu.tsx           # Bottom sheet settings
│   ├── shell-context.tsx           # Global shell state
│   ├── store-view.tsx              # Store analyzer
│   └── thinking-dots.tsx           # AI loading animation
├── lib/
│   ├── supabase/
│   │   ├── client.ts               # Browser Supabase client
│   │   ├── server.ts               # Server Supabase client
│   │   └── middleware.ts           # Session + route protection
│   ├── types.ts                    # Shared TypeScript types
│   └── utils.ts                    # cn(), parseMarkdown(), etc.
├── middleware.ts                    # Next.js middleware
├── supabase/migrations/
│   └── 001_schema.sql              # Full DB schema + RLS + triggers
└── public/
    └── manifest.json               # PWA manifest
```

---

Built by PROSPR · @jexprosper
