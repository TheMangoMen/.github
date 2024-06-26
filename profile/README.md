# WatRank

## Live Code
Frontend: [https://watrank.com](https://watrank.com)

Backend: [https://watrank-api-helguind.csclub.cloud](https://watrank-api-helguind.csclub.cloud)

## Setup Database
1. Clone [https://github.com/TheMangoMen/rankings-db](https://github.com/TheMangoMen/rankings-db)
2. Create `.env` and `.pgpass` files
3. Run `docker compose up -d` - this will create a container running PostgreSQL
4. Run `./setup.sh`
    - `setup.sh` will run various scripts to drop any tables currently in the database, create all tables, constraints, triggers, etc. and loads the sample data in CSV form into the newly created tables.

## Running Backend
1. Clone [https://github.com/themangomen/backend](https://github.com/themangomen/backend)
2. Create `.env` file
3. Run `go run cmd/app/main.go`

## Running Frontend
1. Clone [https://github.com/themangomen/frontend](https://github.com/themangomen/frontend)
2. Run `cd watrank && npm i`
3. Run `npm run dev`

## Features Supported
- View Jobs with Status
- Bulk Import, Watch and Unwatch Jobs
- Upsert Contributions
- Admin Logging

## Testing SQL Statements
The `test-sample.sql` and respective `.out` files are found in [https://github.com/TheMangoMen/rankings-db/tree/main/sql](https://github.com/TheMangoMen/rankings-db/tree/main/sql) under multiple files:
- `test-sample-select-small.sql`
- `test-sample-select-large.sql`
- `test-sample-insert-update-delete.sql`

`sql/sample/jobs_short.csv` was used for these statements for readability of the results.
