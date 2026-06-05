# cPanel (cpanel)

cPanel is a web-based control panel that provides a graphical interface and automation tools to simplify the management of web hosting services. cPanel exposes a family of HTTP APIs (UAPI, WHM API 1, and the legacy cPanel API 2) for automating account, domain, email, database, DNS, and server-wide operations. APIs accept API tokens or Basic Authentication and return JSON or XML responses.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cpanel/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cpanel/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Control Panel
- DNS
- Domains
- Email
- Hosting
- Reseller
- Server Administration
- Web Hosting
- WHM

## Timestamps

- **Created:** 2025-02-09
- **Modified:** 2026-04-28

## APIs

### cPanel UAPI

The cPanel User API (UAPI) is the modern HTTP API for performing cPanel-level operations such as managing email accounts, mailboxes, files, databases, FTP accounts, SSL certificates, and DNS zones for a single cPanel user. UAPI is the recommended replacement for the legacy cPanel API 2.

- **Human URL:** [https://api.docs.cpanel.net/cpanel/introduction/](https://api.docs.cpanel.net/cpanel/introduction/)
- **Base URL:** `https://hostname:2083/execute`

#### Tags

- Databases
- Email
- Files
- Hosting
- REST
- UAPI

#### Properties

- [Documentation](https://api.docs.cpanel.net/cpanel/introduction/)
- [Guide To U A P I](https://api.docs.cpanel.net/guides/guide-to-uapi/)
- [All U A P I Functions](https://api.docs.cpanel.net/openapi/cpanel/tag/Email/)
- [Authentication](https://api.docs.cpanel.net/guides/guide-to-api-authentication/)
- [Postman Collection](collections/cpanel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cpanel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### WHM API 1

The WHM API 1 is the HTTP API for server-wide and reseller-level operations including creating, suspending, and terminating cPanel accounts, managing packages and feature lists, configuring DNS clusters, manipulating reseller privileges, and performing system administration.

- **Human URL:** [https://api.docs.cpanel.net/whm/introduction/](https://api.docs.cpanel.net/whm/introduction/)
- **Base URL:** `https://hostname:2087/json-api`

#### Tags

- Accounts
- Packages
- Reseller
- Server Administration
- WHM

#### Properties

- [Documentation](https://api.docs.cpanel.net/whm/introduction/)
- [Guide To W H M A P I1](https://api.docs.cpanel.net/guides/guide-to-whm-api-1/)
- [API Reference](https://api.docs.cpanel.net/openapi/whm/)
- [Authentication](https://api.docs.cpanel.net/guides/guide-to-api-authentication/)
- [Postman Collection](collections/cpanel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cpanel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### cPanel API 2 (Legacy)

cPanel API 2 is the legacy XML/JSON API for cPanel-user operations. It remains supported for backward compatibility but has been largely superseded by UAPI; new development should target UAPI where possible.

- **Human URL:** [https://api.docs.cpanel.net/cpanel/introduction/](https://api.docs.cpanel.net/cpanel/introduction/)
- **Base URL:** `https://hostname:2083/json-api/cpanel`

#### Tags

- Legacy
- cPanel

#### Properties

- [Documentation](https://api.docs.cpanel.net/cpanel/introduction/)
- [Guide To C Panel A P I2](https://api.docs.cpanel.net/guides/guide-to-cpanel-api-2/)
- [Postman Collection](collections/cpanel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cpanel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Website](https://cpanel.net/)
- [Documentation](https://api.docs.cpanel.net/)
- [Authentication](https://api.docs.cpanel.net/guides/guide-to-api-authentication/)
- [Changelog](https://api.docs.cpanel.net/whm/release-notes/)
- [Forum](https://forums.cpanel.net/)
- [Support](https://support.cpanel.net/)
- [Status Page](https://status.cpanel.net/)
- [Git Hub](https://github.com/CpanelInc)
- [Terms of Service](https://cpanel.net/terms-of-service/)
- [Privacy Policy](https://cpanel.net/privacy-policy/)
- [LinkedIn](https://www.linkedin.com/company/cpanel)
- [Integrations](https://www.cpanel.net/partners/)
- [L L Ms Txt](https://api.docs.cpanel.net/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
