
# WMS Collaboration Portal — Vercel + Supabase Ready

This repository is a static single-file prototype that supports:
- DEMO mode: localStorage (works instantly after deploy or opening index.html)
- LIVE mode: Supabase-backed (real-time) when `SUPABASE_URL` and `SUPABASE_ANON_KEY` are set in Vercel environment variables.

## One-click deploy to Vercel (recommended: smoothest experience)

1. Create a GitHub repo and push this project, or download the ZIP and import to GitHub.
2. Go to Vercel and import the GitHub repo (or click the big deploy button if you host it).
3. In Vercel project > Settings > Environment Variables, add:
   - `SUPABASE_URL` = your supabase project URL (e.g. https://xyz.supabase.co)
   - `SUPABASE_ANON_KEY` = your anon public API key
4. Deploy. Vercel provides a public URL accessible by anyone with the link.

### Supabase setup (quick)
1. Create a free Supabase project: https://app.supabase.com
2. Open SQL Editor and run the following to create the two tables:

```sql
create table prds (
  id text primary key,
  title text,
  body text,
  milestones jsonb,
  created_at timestamptz default now()
);

create table chats (
  id text primary key,
  prd_id text,
  user_name text,
  text text,
  ts bigint,
  created_at timestamptz default now()
);
```

3. For demo ease, temporarily disable RLS or create policies to allow anonymous inserts/selects for these tables. Replace this with stricter policies for production.

### Notes & Next steps
- The static site expects `prds` and `chats` tables to exist in Supabase. When connected, it will read/write directly to Supabase.
- For production-grade usage you should:
  - Add authentication (Supabase Auth / SSO)
  - Harden RLS policies
  - Move file uploads to Supabase Storage or S3
  - Add backup and monitoring

If you want, I can:
- Generate a GitHub-ready repo and push it for you (I cannot push to your GitHub without access).
- Provide a Vercel "Deploy to Vercel" button snippet you can place in the GitHub README for one-click deploy.
- Generate SQL migration files and an init script for Supabase.

