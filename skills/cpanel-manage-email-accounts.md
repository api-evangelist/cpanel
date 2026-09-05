---
name: cpanel-manage-email-accounts
description: >-
  Create, list, quota, forward and delete email accounts on a single cPanel account using UAPI.
  The Email module is the largest surface in UAPI (96 operations) and the most common automation
  target for hosting providers.
api: cPanel UAPI
provider: cPanel
providerId: cpanel
generated: '2026-09-05'
method: generated
source: openapi/_original/cpanel-uapi-openapi.yml
base_url: https://{host}:2083/execute
operations:
  - Email-list_pops
  - Email-count_pops
  - Email-add_pop
  - Email-edit_pop_quota
  - Email-delete_pop
  - Email-add_forwarder
  - Email-delete_forwarder
  - Email-count_forwarders
  - Email-add_auto_responder
  - Email-delete_auto_responder
---

# Manage email accounts with UAPI

Runs against **cPanel UAPI** on port `2083`, scoped to one cPanel account.
Header: `Authorization: cpanel <username>:<APITOKEN>`. Path shape: `/execute/Email/<function>`.

## Before you start

- **Every response is HTTP 200.** Success is `result.status == 1`; failures arrive as
  `result.status == 0` with strings in `result.errors[]`.
- **Roles can disable this whole module.** If the server runs a non-Standard Node profile with the
  *Receive Mail* role off, `Email-list_pops` and its siblings are disabled and return a failure
  envelope — nothing is wrong with your credential. Check the server profile first.
- **Booleans are `1` and `0`.**

## Steps

1. **Inventory.** `Email-list_pops`. Useful parameters: `skip_main=1` to exclude the account's own
   mailbox, `regex=<PCRE>` to filter, `no_validate=1` to skip the mail-database validation check
   when you only need names. `Email-count_pops` gives a count without the payload.
2. **Create a mailbox.** `Email-add_pop` with `email` (the local part), `password`, `domain` and
   optionally `quota`. The contract declares `x-rollback: clean` on this operation — cPanel's own
   signal that it can be undone without loss.
3. **Adjust storage.** `Email-edit_pop_quota` — also `x-rollback: clean`.
4. **Forwarders.** `Email-add_forwarder` / `Email-delete_forwarder`, counted by
   `Email-count_forwarders`. Domain-level forwarding is a separate pair
   (`Email-add_domain_forwarder` / `Email-delete_domain_forwarder`).
5. **Autoresponders.** `Email-add_auto_responder` / `Email-delete_auto_responder`.

## Deleting a mailbox

`Email-delete_pop` is the one operation in the entire cPanel UAPI contract declared
**`x-rollback: lossy`** — cPanel is telling you the mailbox can be removed but something is lost
with it. No recovery window is published. Confirm with the account owner, and confirm a backup
exists, before calling it.

## Paging and sorting

Pagination is off by default. Enable it with
`api.paginate=1&api.paginate_size=100&api.paginate_page=1`; the control block comes back under
`result.metadata.paginate`. When sorting numeric returns you **must** set `api.sort_method`
(`numeric`, `numeric_zero_as_max` or `ipv4`) — cPanel documents that the function fails outright if
you do not.

See `conventions/cpanel-conventions.yml` and `data-model/cpanel-data-model.yml`.
