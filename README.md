# cPanel (cpanel)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
