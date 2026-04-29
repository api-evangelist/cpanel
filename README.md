# cPanel (cpanel)

cPanel is a web-based control panel that provides a graphical interface and automation tools to simplify the management of web hosting services. cPanel exposes a family of HTTP APIs (UAPI, WHM API 1, and the legacy cPanel API 2) for automating account, domain, email, database, DNS, and server-wide operations.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/cpanel/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party
- **x-type:** company

## Tags

- Control Panel, DNS, Domains, Email, Hosting, Reseller, Server Administration, Web Hosting, WHM

## Timestamps

- **Created:** 2025-02-09
- **Modified:** 2026-04-28

## APIs

### cPanel UAPI

The modern HTTP API for cPanel-level operations such as managing email accounts, mailboxes, files, databases, FTP accounts, SSL certificates, and DNS zones.

**Base URL:** `https://hostname:2083/execute`

### WHM API 1

HTTP API for server-wide and reseller-level operations including account creation/suspension/termination, package management, DNS clusters, and reseller privileges.

**Base URL:** `https://hostname:2087/json-api`

### cPanel API 2 (Legacy)

Legacy XML/JSON API for cPanel user operations, retained for backward compatibility but largely superseded by UAPI.

## Common Properties

- [Website](https://cpanel.net/)
- [Documentation](https://api.docs.cpanel.net/)
- [Authentication Guide](https://api.docs.cpanel.net/guides/guide-to-api-authentication/)
- [Change Log](https://api.docs.cpanel.net/whm/release-notes/)
- [Forum](https://forums.cpanel.net/)
- [Support](https://support.cpanel.net/)
- [Status](https://status.cpanel.net/)
- [GitHub](https://github.com/CpanelInc)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
