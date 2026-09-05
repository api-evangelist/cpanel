---
name: cpanel-rotate-api-tokens
description: >-
  Mint, inspect, rename and revoke cPanel and WHM API tokens — the credential rotation flow for any
  automation holding long-lived cPanel access. Covers both token systems, which are separate.
api: cPanel UAPI, WHM API 1
provider: cPanel
providerId: cpanel
generated: '2026-09-05'
method: generated
source: >-
  openapi/_original/cpanel-uapi-openapi.yml, openapi/_original/cpanel-whm-api-openapi.yml,
  https://api.docs.cpanel.net/cpanel/tokens/, https://api.docs.cpanel.net/whm/tokens/
operations:
  - Tokens-create_full_access
  - Tokens-list
  - Tokens-rename
  - Tokens-revoke
  - Tokens-api_token_create
  - Tokens-api_token_list
  - Tokens-api_token_get_details
  - Tokens-api_token_update
  - Tokens-api_token_revoke
---

# Rotate cPanel and WHM API tokens

cPanel has **two independent token systems** and they do not share a namespace, a header prefix or
an API. Decide which one you are rotating before you start.

| | cPanel account token | WHM token |
|---|---|---|
| API | UAPI, port 2083 | WHM API 1, port 2087 (or 443 via a service subdomain) |
| Header | `Authorization: cpanel <user>:<TOKEN>` | `Authorization: whm <user>:<token>` |
| Holder | one cPanel account | root or a reseller |
| Create | `Tokens-create_full_access` | `Tokens-api_token_create` |
| Revoke | `Tokens-revoke` | `Tokens-api_token_revoke` |

Neither prefix is `Bearer`. A client that sends `Bearer` will be rejected.

## Rotation steps

1. **Inventory.** `Tokens-list` (UAPI) or `Tokens-api_token_list` (WHM). On WHM,
   `Tokens-api_token_get_details` returns one token's detail.
2. **Mint the replacement first.** `Tokens-create_full_access` with a `name`, or
   `Tokens-api_token_create` with `token_name` and optionally `acl`, `expires_at` and `whitelist_ip`.
   The UAPI equivalent takes `name` and optionally `expires_at` and `readonly`.
   **Capture the token from this response.** cPanel warns that the value cannot be retrieved after
   you navigate away — there is no read-back operation.
3. **Cut over.** Deploy the new token to the caller and confirm a live call succeeds
   (`metadata.result == 1` on WHM, `result.status == 1` on UAPI).
4. **Revoke the old one.** `Tokens-revoke` or `Tokens-api_token_revoke`. This is the reversal pair
   for step 2; the create is not otherwise undoable because the secret is unrecoverable.
5. **Renaming is not rotation.** `Tokens-rename` (UAPI, declared `x-rollback: clean`) and
   `Tokens-api_token_update` (WHM) change metadata, not the secret.

## Expiry does not clean up after itself

cPanel documents that an **expired WHM API token is not removed** — the system leaves it in place
and you must delete it by hand. Include a sweep of expired tokens in the rotation job, or they
accumulate.

## Two traps worth knowing

- **`Tokens-create_full_access` means what it says.** It mints a token with full access to the
  cPanel account. cPanel's finer-grained restriction lives in WHM token privileges and the
  reseller permission model, not in an OAuth scope — there is no scope vocabulary for these APIs
  (see `scopes/cpanel-scopes.yml`).
- **Access hashes are not a modern alternative.** `Resellers-accesshash` and
  `Resellers-get_remote_access_hash` are both marked `deprecated: true` in the contract, even
  though access-hash authentication is still described in the auth guide.

## Lockout risk

cPanel & WHM ships cPHulk, which blocks repeated failed authentication. A rotation that deploys a
bad token and retries in a loop will get the source IP blocked — that failure looks like a rate
limit but is not one (`rate-limits/cpanel-rate-limits.yml`). Verify one call before rolling out.
