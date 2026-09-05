---
name: cpanel-provision-mysql-database
description: >-
  Create a MySQL database and user, grant privileges, verify, and tear the pair down again on a
  single cPanel account with UAPI. The standard database bootstrap for an application deploy.
api: cPanel UAPI
provider: cPanel
providerId: cpanel
generated: '2026-09-05'
method: generated
source: openapi/_original/cpanel-uapi-openapi.yml
base_url: https://{host}:2083/execute
operations:
  - Mysql-get_restrictions
  - Mysql-get_server_information
  - Mysql-create_database
  - Mysql-create_user
  - Mysql-set_privileges_on_database
  - Mysql-get_privileges_on_database
  - Mysql-list_databases
  - Mysql-list_users
  - Mysql-setup_db_and_user
  - Mysql-revoke_access_to_database
  - Mysql-delete_user
  - Mysql-delete_database
  - Mysql-set_password
---

# Provision a MySQL database and user

UAPI on port `2083`, scoped to one cPanel account.
Header: `Authorization: cpanel <username>:<APITOKEN>`.

## Before you start

- **Name length is constrained and the constraint is discoverable.** Call
  `Mysql-get_restrictions` first — cPanel prefixes database and user names with the cPanel account
  name, so the usable length is shorter than MySQL's own limit. Guessing here is the most common
  failure in this flow.
- `Mysql-get_server_information` tells you which MySQL server and version you are actually
  talking to (it may be remote — see `Mysql-locate_server`).
- **Every response is HTTP 200.** Check `result.status`.

## Steps

1. `Mysql-get_restrictions` — read the name-length limits.
2. `Mysql-create_database` with `name`.
3. `Mysql-create_user` with `name` and `password`.
4. `Mysql-set_privileges_on_database` with `user`, `database` and the privilege list.
5. Verify with `Mysql-get_privileges_on_database`, and confirm the objects exist with
   `Mysql-list_databases` and `Mysql-list_users`.

**Shortcut:** `Mysql-setup_db_and_user` creates a randomly named database/user pair in one call.
Use it when the names do not matter; use the explicit sequence when they do.

## Remote access

If the application runs off-box, `Mysql-add_host` enables remote access for a host and
`Mysql-add_host_note` annotates why. `Mysql-delete_host` reverses it. Add the host only after the
grant exists, and remove it when the application moves.

## Teardown, in order

`Mysql-revoke_access_to_database` → `Mysql-delete_user` → `Mysql-delete_database`.

None of these three carries an `x-rollback` declaration in the contract, and none has a published
recovery window. **`Mysql-delete_database` destroys the data.** Take a dump first —
`Mysql-dump_database_schema` returns the schema only, so a real backup means the cPanel Backup
module (`Backup-fullbackup_to_homedir` and friends) or a mysqldump outside the API.

## Rotating a password

`Mysql-set_password` changes the MySQL user's password in place. Coordinate it with the
application's own credential rollout — there is no dual-credential window.

See `conventions/cpanel-conventions.yml` for the response envelope and control variables.
