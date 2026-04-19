# Security Policy

SquadFlow is a documentation project, not executable software. "Security" here covers:

- Accidental disclosure of sensitive information (real client data, credentials, proprietary playbooks) in any file of this repository.
- Guidance in the documentation that could lead adopters to insecure configurations (e.g., exposing secrets in Notion, weak governance patterns).
- Vulnerabilities in the helper scripts under `scripts/` (e.g., the Notion publication pipeline).

## Reporting a vulnerability or sensitive disclosure

**Preferred channel: GitHub Security Advisories (private, encrypted).**

1. Go to the repository's [Security tab](https://github.com/guilhermej/squadflow-framework/security).
2. Click **Report a vulnerability**.
3. Fill the form. Your report is visible only to maintainers until disclosure.

This is the fastest and safest path for anything that should not be public yet.

## Email fallback

If, for some reason, you cannot use GitHub Security Advisories, you may contact the maintainer directly at:

`guilherme[at]solyd[.]com[.]br`

Please include the word **"squadflow-security"** in the subject so the message isn't filtered.

## Scope

In scope:

- Sensitive data leaks in examples, templates, or diagrams.
- Misleading guidance that could harm adopters (e.g., insecure Notion permissions, missing data-handling advice).
- Vulnerabilities in `scripts/*.py` (injection, path traversal, credential handling).
- Supply-chain issues in `requirements.txt` or GitHub Actions workflows.

Out of scope:

- Typos and non-security bugs — open a normal issue.
- Disagreements with framework design choices — open a feature-request issue.
- Third-party services SquadFlow integrates with (Notion, GitHub) — report to those vendors directly.

## Response time

- Acknowledgment within **5 business days**.
- Initial assessment within **10 business days**.
- Resolution timeline depends on severity; you will be updated throughout.

## Disclosure

Once a fix is merged, we publish a Security Advisory with:

- A description of the issue
- Affected versions (if applicable)
- The fix
- Credit to the reporter (if they consent)

## Hall of thanks

Contributors who responsibly disclose security issues are credited here after public disclosure.

> No reports yet.
