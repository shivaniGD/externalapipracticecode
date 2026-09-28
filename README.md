# Next.js: Public API + .env.local

## Tasks covered
1. **API chosen:** JSONPlaceholder. Docs: https://jsonplaceholder.typicode.com/guide/
   This project uses the `GET /users` endpoint.
2. **Config in `.env.local`:** `API_BASE_URL` and `API_KEY`, read via `process.env` and never hard-coded.
   `.env.example` is the committed template with no secrets.
3. **Live data:** `pages/index.js` fetches `/users` in `getServerSideProps` and renders a table.
4. **`.env.local` excluded from git:** see below.

## Run
```bash
npm install
npm run dev
```
Restart the dev server after editing `.env.local`; Next.js only reads it at startup.

## Env variable rules
- No prefix (`API_KEY`): server-only, safe for secrets. Available in `getServerSideProps` and API routes.
- `NEXT_PUBLIC_` prefix: inlined into browser JavaScript, so never put secrets there.

## Confirm .env.local is ignored before committing
```bash
git init
npm run check:env      # prints the .gitignore rule that matches: OK
git add .
git status             # .env.local must NOT be listed
```
If `check:env` prints nothing, the file is not ignored. Fix `.gitignore` before your first commit.
If a secret was ever committed, ignoring it later is not enough: rotate the key.
