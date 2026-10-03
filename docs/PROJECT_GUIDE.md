# ArgentBank — project guide

Express/MongoDB backend for the Argent Bank training application, with signup, login and authenticated profile endpoints.

## Scope and source

This guide describes the default branch `main` reviewed on 3 October 2026. Commands were checked against committed manifests and configuration; applications and external integrations were not executed as part of this documentation update.

## Repository map

- `server/server.js`
- `server/routes/userRoutes.js`
- `server/controllers/userController.js`
- `server/database/connection.js`
- `server/scripts/populateDatabase.js`
- `swagger.yaml`
- `CONTRIBUTING.md`

## Prerequisites and local use

Clone the repository and enter its root directory:

```sh
git clone https://github.com/sarabranco92/ArgentBank.git
cd ArgentBank
```

### Database and server

Configure a root `.env` with your own values:

```dotenv
DATABASE_URL=mongodb://127.0.0.1:27017/argentBankDB
PORT=3001
SECRET_KEY=replace-with-a-long-random-secret
```

```sh
npm install
npm run dev:server
```

In a second terminal, from the repository root:

```sh
npm run populate-db
```

Seeding creates demo users in the configured database. Use a disposable development database. For a non-watching server use `npm run server`.

### Implemented user API

| Method | Path | Authentication |
| --- | --- | --- |
| POST | `/api/v1/user/signup` | Public |
| POST | `/api/v1/user/login` | Public |
| POST | `/api/v1/user/profile` | Bearer token |
| PUT | `/api/v1/user/profile` | Bearer token |

The frontend requests a `userName` update; confirm the backend’s accepted fields before assuming these separate repositories are fully compatible.

## Available npm scripts

From the repository root unless a directory is explicitly specified. These are existing commands, not evidence of a successful run.

| Command | Committed behavior |
| --- | --- |
| `npm run dev:server` | `nodemon ./server/server.js` |
| `npm run populate-db` | `node ./server/scripts/populateDatabase.js` |
| `npm run server` | `node ./server/server.js` |

## Configuration and implementation notes

This is the backend; the separate `argent-bank` repo is the React frontend. Swagger at `/api-docs` is exposed only outside production. No npm test script is defined. The existing README’s Node 12 guidance is historical, not a recommendation to deploy an unsupported runtime. The transaction Swagger design is not evidence of implemented transaction endpoints.

## Verification checklist

Start a disposable local MongoDB database, seed only that database, log in with a demo user and exercise authenticated profile retrieval/update. Confirm unauthenticated requests are rejected.

No dedicated automated test/spec files were found in the reviewed application tree. Where a test script exists, its presence alone does not establish test coverage.

## Maintenance

Keep this guide in sync when routes, commands, environment variables or hosting paths change. Use development databases/accounts for integration checks. Keep private credentials in server-side environment configuration and out of documentation. No new license or ownership terms are introduced by this guide; retain existing repository notices.
