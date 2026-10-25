# Deploy checklist: GitHub → Neon → Render

Render → your web service → Environment → Edit. Exact key names, no quotes, no extra spaces.

| Key | Value |
|---|---|
| `SPRING_PROFILES_ACTIVE` | `prod` (ends with ACTIVE, not ACTIVATE) |
| `DB_URL` | `jdbc:postgresql://YOUR_NEON_HOST/neondb?sslmode=require` (Neon → Connect, **Connection pooling OFF**, host only) |
| `DB_USERNAME` | Neon role, e.g. `neondb_owner` |
| `DB_PASSWORD` | Neon role password (Show password) – not your Neon website password |
| `JWT_SECRET` | output of `openssl rand -base64 32` (or the Node.js command in README) |

Render settings: Runtime = Docker, Instance type = Free, Health Check Path = `/actuator/health`,
Docker command override = blank.

After "Live": open the service URL, check `/actuator/health` → `{"status":"UP"}`,
and register a new practice account (local data is not copied to Neon).

Never commit DB_PASSWORD or JWT_SECRET to GitHub.
