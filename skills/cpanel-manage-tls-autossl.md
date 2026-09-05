---
name: cpanel-manage-tls-autossl
description: >-
  Diagnose and repair TLS coverage on a cPanel account — inspect installed certificates, find the
  domains AutoSSL is failing on and why, exclude or re-include domains, and install a certificate
  by hand when automated issuance cannot pass domain control validation.
api: cPanel UAPI, WHM API 1
provider: cPanel
providerId: cpanel
generated: '2026-09-05'
method: generated
source: >-
  openapi/_original/cpanel-uapi-openapi.yml, openapi/_original/cpanel-whm-api-openapi.yml
operations:
  - SSL-installed_hosts
  - SSL-list_certs
  - SSL-fetch_cert_info
  - SSL-get_autossl_problems
  - SSL-get_autossl_renewal_status
  - SSL-is_autossl_check_in_progress
  - SSL-get_autossl_excluded_domains
  - SSL-add_autossl_excluded_domains
  - SSL-remove_autossl_excluded_domains
  - SSL-install_ssl
  - SSL-generate_key
  - SSL-generate_csr
  - DCV-check_domains_via_dns
  - DCV-check_domains_via_http
  - SSL-get_autossl_problems_for_domain
  - SSL-get_autossl_problems_for_user
  - SSL-get_autossl_providers
  - SSL-get_autossl_log
---

# Diagnose and fix TLS coverage

Two surfaces are involved. Account-level work is **UAPI** on port `2083`; server-level AutoSSL
administration is **WHM API 1** on port `2087`. Both answer HTTP 200 on failure — check
`result.status` (UAPI) or `metadata.result` (WHM).

## 1. See what is actually installed

- `SSL-installed_hosts` — domains with certificate information attached.
- `SSL-list_certs` — every certificate on the account.
- `SSL-fetch_cert_info` — one certificate's detail.
- `SSL-can_ssl_redirect` — whether domains can be redirected to their secure URL.

## 2. Find out why AutoSSL is not covering a domain

- `SSL-get_autossl_problems` (UAPI) lists the domains with problems.
- `SSL-get_autossl_renewal_status` gives one domain's renewal state.
- `SSL-is_autossl_check_in_progress` — do not diagnose mid-run; wait for it to finish.
- On the server side, `SSL-get_autossl_problems_for_domain` and
  `SSL-get_autossl_problems_for_user` (WHM API 1) return DCV issues, and `SSL-get_autossl_log`
  returns the AutoSSL log contents.

Almost every AutoSSL failure is a **domain control validation** failure. Test it directly:
`DCV-check_domains_via_http` and `DCV-check_domains_via_dns` tell you whether the domain can pass
DCV at all, which separates "DNS is wrong" from "AutoSSL is misconfigured".

`SSL-get_autossl_providers` (WHM) shows which issuer is configured — the provider metadata carries
the ACME account and the provider's terms-of-service URL.

## 3. Exclude what genuinely cannot pass

A domain that will never resolve to this server will fail AutoSSL forever and fill the log.
`SSL-add_autossl_excluded_domains` excludes it; `SSL-remove_autossl_excluded_domains` puts it back;
`SSL-get_autossl_excluded_domains` shows the current list. This pair is a clean reversal — use it
instead of disabling AutoSSL wholesale (`SSL-disable_autossl` on WHM), which turns off renewal for
everything.

## 4. Install a certificate by hand

When you hold a certificate from elsewhere: `SSL-generate_key` → `SSL-generate_csr` → (issue
outside cPanel) → `SSL-install_ssl` with the certificate, key and CA bundle.
`SSL-fetch_key_and_cabundle_for_certificate` retrieves the matching material later, and
`SSL-set_cert_friendly_name` labels it — SSL is one of the few cPanel entities with a real `id`
and a `friendly_name`, so label certificates you install programmatically.

## Cautions

- `SSL-check_shared_cert` is marked `deprecated: true` in the contract. Do not build on it.
- `SSL-delete_ssl`, `SSL-delete_cert` and `SSL-delete_key` remove TLS from a live domain
  immediately. No rollback is declared and no recovery window is published; re-issuing means
  passing DCV again, which can take time you do not have while the site is serving errors.
- `SSL-rebuildssldb` and `SSL-rebuild_mail_sni_config` start background rebuilds — they return
  before the work finishes, so poll rather than assuming completion.
