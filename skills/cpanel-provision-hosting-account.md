---
name: cpanel-provision-hosting-account
description: >-
  Provision, inspect, suspend, unsuspend and remove a cPanel hosting account on a WHM server,
  using the hosting plan (package) system. This is the core account-lifecycle flow for anyone
  reselling or automating cPanel hosting.
api: WHM API 1
provider: cPanel
providerId: cpanel
generated: '2026-09-05'
method: generated
source: openapi/_original/cpanel-whm-api-openapi.yml
base_url: https://{host}:2087/json-api
operations:
  - Packages-listpkgs
  - Packages-getpkginfo
  - Accounts-createacct
  - Accounts-accountsummary
  - Accounts-listaccts
  - Accounts-modifyacct
  - Accounts-changepackage
  - Accounts-suspendacct
  - Accounts-unsuspendacct
  - Accounts-removeacct
  - Accounts-get_current_users_count
  - Accounts-get_maximum_users
---

# Provision a cPanel hosting account

Runs against **WHM API 1** on the customer's own server, port `2087`.
Every call needs `api.version=1` and an `Authorization: whm <username>:<token>` header.

## Before you start

- **Every response is HTTP 200.** The outcome is `metadata.result` — `1` success, `0` failure, with
  `metadata.reason` carrying the message. Do not branch on the status code.
- **Booleans are `1` and `0`.** `true`/`false` are rejected.
- Wrong port is an authentication failure: cPanel ports (2082/2083) will not serve this API.

## Steps

1. **Check headroom.** `Accounts-get_current_users_count` and `Accounts-get_maximum_users` —
   the licence caps how many accounts this server may hold (see `plans/cpanel-plans-pricing.yml`;
   the licence tier is priced by account count). Creating past the cap fails.
2. **Pick a hosting plan.** `Packages-listpkgs` returns the plans available to the calling user;
   `Packages-getpkginfo` returns one plan's configuration. The plan sets quotas and the feature
   list the new account inherits.
3. **Create the account.** `Accounts-createacct`. Only `username` is required by the contract;
   in practice pass `domain`, `password` and `pkg` (the hosting plan) as well, plus
   `contactemail`, `featurelist` and `bwlimit` where the plan does not already set them.
   - This is a **GET**. Do not let an HTTP client retry it on timeout — there is no
     `Idempotency-Key` on this API and a retry creates a second account or fails messily.
   - The contract declares no rollback for this operation. The reversal is
     `Accounts-removeacct`, which is destructive, not an undo.
4. **Verify.** `Accounts-accountsummary` with `user=<username>`. Confirm `metadata.result == 1`
   and the returned quota and plan match what you asked for.
5. **Amend rather than recreate.** `Accounts-modifyacct` for account fields,
   `Accounts-changepackage` to move the account onto a different plan.

## Suspending instead of deleting

`Accounts-suspendacct` and `Accounts-unsuspendacct` are a genuine reversible pair, and
`Accounts-listsuspended` shows what is currently held. Prefer suspension for non-payment or abuse:
it is reversible, and account deletion is not.

## Deletion, and what it costs

`Accounts-removeacct` deletes the account and its data. There is **no undo and no published
recovery window** — recovery means restoring from a backup that already exists
(`Backup-restoreaccount`, `Backup-restore_queue_add_task`, `Transfers-start_local_cpmove_restore`),
and backup retention is set by the server operator, not by cPanel. Confirm a restorable backup
before deleting anything you might want back.

## Listing at scale

`Accounts-listaccts` returns every account with no paging by default. Use the chunking variables:
`api.chunk.enable=1&api.chunk.size=100&api.chunk.start=1` (`start` is 1-indexed). Filter with
`api.filter.enable=1&api.filter.a.field=<return>&api.filter.a.arg0=<value>&api.filter.a.type=eq`,
and trim the payload with `api.columns.enable=1&api.columns.a=user&api.columns.b=domain`.

See `conventions/cpanel-conventions.yml` for the full control-variable grammar and
`errors/cpanel-problem-types.yml` for the failure envelope.
