# MTA-STS Policy for starknet.org

This repository hosts the MTA-STS (RFC 8461) policy file for starknet.org,
served via GitHub Pages at:

https://mta-sts.starknet.org/.well-known/mta-sts.txt

## Owner

Security & IT, Starknet Foundation

## Repository visibility

This repository is private by default. The policy file it serves is public
via GitHub Pages at the URL above. Keeping the source private reduces
reconnaissance surface (commit history, contributor patterns, tooling
signals) without affecting the served content. External auditors can be
granted read access on request.

## How updates work

Policy changes require two coordinated steps:

1. Edit `.well-known/mta-sts.txt` via pull request, get review, merge to `main`
2. Update the `_mta-sts` TXT record in GoDaddy DNS with a new `id` value
   (UTC timestamp format: YYYYMMDDTHHMMSSZ)

Both steps are required. External mail servers re-fetch the policy only when
the `id` in DNS changes. Without step 2, cached policies persist for up to
`max_age` seconds (currently 7 days).

## Current state

- Mode: testing (as of initial deployment)
- Planned transition to enforce mode: 14 days after initial publication,
  contingent on clean TLS reports

## Break-glass: disable MTA-STS

Remove the `_mta-sts` TXT record from DNS in GoDaddy. Cached policies expire
per `max_age` (7 days). Senders that don't support MTA-STS are unaffected.

## TLS reports

Sent daily to: smtp-tls-reports@starknet.org

## References

- RFC 8461 (MTA-STS): https://tools.ietf.org/html/rfc8461
- RFC 8460 (TLS reporting): https://tools.ietf.org/html/rfc8460
- Google Workspace MTA-STS setup:
  https://knowledge.workspace.google.com/admin/gmail/advanced/about-mta-sts-and-tls-reporting
