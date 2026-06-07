# forms.moddy.app

Single-page Tally form embed with Discord authentication.

## How it works

Each URL `https://forms.moddy.app/{formId}` :

1. Checks authentication via `GET /auth/me` — redirects to `moddy.app/sign-in` if not logged in
2. Checks the form exists via `GET /tally/forms/{formId}` — shows a 404 page if not
3. Fetches a session hash via `GET /tally/session-hash`
4. Embeds the Tally form with `discord_id`, `email` and `session` as hidden fields

## Stack

- Vanilla HTML/JS, no build step
- [Material Web](https://material-web.dev/) for loading spinners
- Hosted on Vercel (`vercel.json` rewrites all routes to `index.html`)

## Local dev

```bash
npx serve .
# → http://localhost:3000/{formId}
```

## Environment

The frontend has no environment variables. It calls:

| Endpoint | Purpose |
|---|---|
| `https://api.moddy.app/auth/me` | Auth check |
| `https://api.moddy.app/tally/forms/{formId}` | Form metadata |
| `https://api.moddy.app/tally/session-hash` | HMAC session hash |

The backend must allow credentials from `https://forms.moddy.app` in its CORS policy.
