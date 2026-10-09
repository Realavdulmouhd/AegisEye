# Security

AegisEye is a research prototype. It must not be connected to live physical access hardware or used to make operational identity decisions.

## Vulnerability reports

Please don't publish working exploits, credentials, or biometric samples in public GitHub issues. Contact the maintainer through their GitHub profile to arrange a private report.

Include the affected component, reproducible steps using synthetic data, the expected and observed behavior, and redacted logs when available.

## Sensitive data

Do not commit raw face or eye images, voice recordings, template encryption keys, application secrets, database exports, or personal biometric vectors.

If a secret is exposed, deleting it from the latest commit is not enough. Revoke it, examine repository history, and consider copies already fetched by others.

## Areas under active hardening

Enrollment authorization, replay resistance, liveness validation, audit integrity, matching evaluation, and separation between experimental acquisition and access decisions.
