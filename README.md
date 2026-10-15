# ChatWave — real-time messaging starter

A responsive iMessage-inspired messaging app built with Next.js, React and Supabase. This is an application starter, not a hosted/production-ready service.

## Included

- Email/password sign-up and sign-in using Supabase Auth
- Profile names created on sign-up
- Start a direct conversation using another registered user's email
- Persistent message storage
- Realtime incoming messages via Supabase Realtime
- Row Level Security (RLS) policies for conversation membership and messages
- Responsive desktop and mobile layouts
- Conversation search, details panel and emoji shortcut

## Requirements

- Node.js 20 or later
- A Supabase project
- A deployment account such as Vercel for a public website

## 1. Configure Supabase

1. Create a project at https://supabase.com/dashboard.
2. In the project, open SQL Editor.
3. Run the contents of `supabase/schema.sql`.
4. In Project Settings → API, copy the Project URL and the publishable/anon key.
5. In Authentication settings, configure your site's allowed redirect URLs. For local development, add `http://localhost:3000`.
6. Decide whether to require email confirmation. If enabled, users must confirm their email before signing in.
7. In Database → Replication/Realtime, verify the `messages` table is included in the `supabase_realtime` publication.

## 2. Run locally

```bash
cp .env.example .env.local
```

Edit `.env.local` and set:

```text
NEXT_PUBLIC_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY
```

Then run:

```bash
npm install
npm run dev
```

Open http://localhost:3000.

## 3. Test with two people

1. Open the app in a normal browser and create an account.
2. Open a private/incognito window or a second browser/device and create a second account with a different email.
3. From the first account, choose **New conversation** and enter the second account's registered email.
4. Send messages in both directions.

If email confirmation is enabled, confirm both accounts before signing in.

## 4. Deploy

A straightforward option is Vercel:

1. Put this project in a private Git repository.
2. Import the repository into https://vercel.com.
3. Add `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` as project environment variables.
4. Deploy.
5. Add the deployed site URL to Supabase Authentication's allowed URLs and redirect URLs.
6. Test sign-up, conversation creation, access isolation and real-time messaging on two separate devices.

## Important security and product notes

- Never put a Supabase service-role key in browser code or any `NEXT_PUBLIC_` variable. This starter does not need one.
- RLS is essential. Review policies and test that a user cannot read messages in a conversation they do not belong to before launching.
- The `start_conversation` function uses a registered email to locate a recipient. This is a simple MVP approach; for a public product, add rate limits, anti-enumeration protections, blocking/reporting and invitation/username flows.
- This app does **not** implement end-to-end encryption. Supabase transport/storage security and RLS are not the same as end-to-end encryption. Do not advertise the app as end-to-end encrypted.
- The MVP does not include push notifications, media uploads, message editing/deletion, delivery/read receipts, group chats, blocking/reporting, abuse monitoring or account recovery UI.
- Add CAPTCHA/rate limiting, email abuse controls, privacy policy, terms, retention/deletion procedures and monitoring before public launch.
- Do not use real sensitive information while testing.

## Next recommended milestones

1. Add user search by username and friend/contact requests.
2. Add conversation last-message previews with server-side query optimization.
3. Add unread counts and read receipts.
4. Add secure image/file uploads with private storage policies.
5. Add push notifications.
6. Conduct a security review and penetration tests before a public release.
7. Design and implement a reviewed end-to-end encryption protocol if that is a product requirement; do not invent your own cryptography.
