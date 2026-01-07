# nextjs-ecommerce-docker-starter
🛒 Modern e-commerce starter with Next.js 16, TypeScript, PostgreSQL &amp; Docker.  Features: Product catalog, shopping cart (localStorage), Drizzle ORM, Tailwind CSS 4,  and full Docker Compose setup for local development. Ready to clone and customize.

# 1-ecommerce (Docker + PostgreSQL + Drizzle)

E-commerce demo built with Next.js (App Router) with product catalog from PostgreSQL via Drizzle ORM.

## Containers (numbered naming)

The [compose.yaml](compose.yaml) file creates these containers:

- `1_ecommerce_postgres`
- `2_ecommerce_web`
- `3_ecommerce_drizzle_studio`

## Prerequisites

- Docker Desktop installed and running
- Node.js 20+ (for commands outside Docker, optional)

If you see an error like `dockerDesktopLinuxEngine ... The system cannot find the file specified`, it usually means Docker Desktop is not running.

## Start everything with Docker

1. (Optional) Copy environment file

```powershell
Copy-Item .env.example .env
```

1. Build + start Postgres

```powershell
docker compose up -d postgres
```

1. Run migrations + seed (executes inside compose network)

```powershell
docker compose run --rm web npm run db:migrate
docker compose run --rm web npm run db:seed
```

1. Start app + Drizzle Studio

```powershell
docker compose up -d web drizzle-studio
```

## URLs

- App: <http://localhost:3000>
- Drizzle Studio (UI): <https://local.drizzle.studio?host=localhost>

Note: Recent versions of `drizzle-kit studio` may return `404 Not Found` at `http://localhost:4983/`.
In this case, port `4983` is the local connector, and the interface opens at `https://local.drizzle.studio`.

## Useful scripts

- `npm run db:generate` (generate migrations from schema)
- `npm run db:migrate` (apply migrations)
- `npm run db:seed` (insert demo products)
- `npm run db:studio` (open Drizzle Studio)

## Main structure

- [src/db/schema.ts](src/db/schema.ts): Drizzle schema (`products` table)
- [src/db/seed.ts](src/db/seed.ts): product seeding
- [src/app/products](src/app/products): listing + details
- [src/app/cart](src/app/cart): shopping cart (localStorage)

## Tech Stack

- **Next.js 16** - App Router, React Server Components, Turbopack
- **TypeScript 5** - Strict mode enabled
- **Tailwind CSS 4** - Modern utility-first CSS
- **PostgreSQL 16** - Relational database (Alpine)
- **Drizzle ORM** - Type-safe SQL with migrations
- **Docker Compose** - Multi-container orchestration
- **React 19** - Latest React features

## Features

✅ Product catalog with database integration
✅ Dynamic product detail pages
✅ Shopping cart with localStorage
✅ Reactive cart updates (useSyncExternalStore)
✅ Dark mode support
✅ Fully Dockerized development environment
✅ Type-safe database queries
✅ Hot-reload in Docker

## Deployment on a new machine

```powershell
# 1. Clone repository
git clone your-repo.git
cd 1-ecommerce

# 2. Create environment file
Copy-Item .env.example .env

# 3. Install dependencies
npm install

# 4. Start containers
docker compose up -d

# 5. Run migrations and seed
docker exec 2_ecommerce_web npm run db:migrate
docker exec 2_ecommerce_web npm run db:seed
```

Your app will be running at <http://localhost:3000> 🚀

## Development

The project uses bind mounts, so changes to source code will trigger hot-reload automatically.

To rebuild after dependency changes:

```powershell
docker compose down
docker compose build
docker compose up -d
```

## Database Management

Access Drizzle Studio at <https://local.drizzle.studio?host=localhost> to:

- View and edit data visually
- Inspect schema and relationships
- Run queries safely

## License

MIT
