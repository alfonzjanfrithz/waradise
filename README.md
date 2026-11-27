# Waradise

Online store built with [Medusa](https://medusajs.com) v2 (TypeScript) as the open-source commerce backend (product catalog, cart, checkout, and admin API) and a Next.js storefront in front of it.

## Project layout

- `store/apps/backend` — Medusa v2 server and admin dashboard (`http://localhost:9000/app`)
- `store/apps/storefront` — Next.js starter storefront (`http://localhost:8000`)

## Local setup

### Prerequisites

- Node.js v22.22+
- `pnpm` v10+
- PostgreSQL 15+

### 1. Start PostgreSQL and create the database

On Fedora:

```bash
sudo dnf install -y postgresql-server
sudo postgresql-setup --initdb
sudo systemctl enable --now postgresql
sudo -u postgres createdb medusa_store
```

On Ubuntu/Debian:

```bash
sudo apt-get update && sudo apt-get install -y postgresql postgresql-client
sudo service postgresql start
sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'postgres';"
sudo -u postgres createdb medusa_store
```

Or with Docker / Podman:

```bash
docker run -d --name waradise-postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=medusa_store \
  -p 5432:5432 \
  postgres:16-alpine
```

### 2. Install dependencies

```bash
cd store
pnpm install
```

### 3. Configure the backend and run migrations

```bash
cp apps/backend/.env.template apps/backend/.env
```

Update `apps/backend/.env` with your PostgreSQL `DATABASE_URL` and random values for `JWT_SECRET` and `COOKIE_SECRET` (for example via `openssl rand -hex 32`). Keep `.env` out of git.

Run migrations (this also seeds the default `MYR` currency, `Malaysia` region, and starter data) and create an admin user:

```bash
cd apps/backend
pnpm exec medusa db:migrate
pnpm exec medusa user -e admin@example.com -p supersecret
```

### 4. Start the Medusa backend

```bash
cd store/apps/backend
pnpm dev
```

Open the admin dashboard at `http://localhost:9000/app`, sign in, and copy your publishable API key from **Settings > Publishable API Keys**.

### 5. Configure and start the Next.js storefront

```bash
cp store/apps/storefront/.env.template store/apps/storefront/.env.local
```

Set `NEXT_PUBLIC_MEDUSA_PUBLISHABLE_KEY` in `store/apps/storefront/.env.local` to the key copied from Medusa Admin (`NEXT_PUBLIC_DEFAULT_REGION` defaults to `my` for Malaysia / MYR).

Start the storefront:

```bash
cd store/apps/storefront
pnpm dev
```

The storefront runs at `http://localhost:8000` (Malaysia region at `http://localhost:8000/my`).

You can also run both backend and storefront together from `store/`:

```bash
cd store
pnpm dev
```
