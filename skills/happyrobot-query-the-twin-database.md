---
name: Explore and query the Twin database safely
description: Introspect the schema of a Happyrobot Twin database, read rows, and write with the narrowest operation rather than reaching for arbitrary SQL.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - GET /twin/schema
  - GET /twin/tables/{tableName}
  - POST /twin/sql
  - POST /twin/tables
  - POST /twin/tables/{tableName}/rows
  - PATCH /twin/tables/{tableName}/rows
  - DELETE /twin/tables/{tableName}/rows
  - POST /twin/dump
---

# Explore and query the Twin database

Twin is a customer-owned relational store inside the Happyrobot platform, scoped to the organization on
your API key. Tables are addressed by **name**, not UUID.

## Read first

1. `GET /twin/schema` — all tables and views with columns, types and primary keys. Always start here;
   never assume a column exists.
2. `GET /twin/tables/{tableName}` — fetch rows with pagination.
3. `POST /twin/dump` — bulk export.

## Prefer the narrow operation over arbitrary SQL

`POST /twin/sql` executes arbitrary SQL — `SELECT`, `INSERT`, `UPDATE`, `DELETE` **and DDL**. It is
powerful and unguarded. Use the typed operations whenever they cover the job:

| Intent | Use this | Not this |
|---|---|---|
| Insert one row | `POST /twin/tables/{tableName}/rows` | `POST /twin/sql` |
| Update matching rows | `PATCH /twin/tables/{tableName}/rows` | `POST /twin/sql` |
| Delete by primary key | `DELETE /twin/tables/{tableName}/rows` | `POST /twin/sql` |
| Create a table | `POST /twin/tables` | `POST /twin/sql` |
| Read rows | `GET /twin/tables/{tableName}` | `POST /twin/sql` |

Reserve `POST /twin/sql` for genuine multi-table queries and aggregations.

## Destructive operations

- `DELETE /twin/tables/{tableName}` drops a table permanently.
- `POST /twin/sql` can drop or truncate anything in the schema.

Both are reachable under the same single `mcp:full` scope as every read-only tool on the Twin MCP server
(`https://mcp.platform.happyrobot.ai/twin/mcp`, tools `execute_sql` and `drop_table`). **There is no
read-only scope.** If you are running as an autonomous agent:

1. Take a `POST /twin/dump` before any DDL or bulk delete.
2. Run the `SELECT` form of a destructive statement first and check the row count.
3. Require explicit human confirmation before `DELETE /twin/tables/{tableName}` or any DDL through
   `POST /twin/sql`.

## Errors

- Envelope is `{ error, message, statusCode, details }`.
- `400` for malformed SQL or a bad column type.
- `401` for a bad key; `403` if the table belongs to another organization.
- No idempotency key exists: a retried `POST /twin/tables/{tableName}/rows` inserts a second row unless
  the table has a unique constraint.
