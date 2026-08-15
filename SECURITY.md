# Security Policy

## Supported versions

Semaphore security fixes are provided for the **current latest stable release**.

At the time of this policy update, the supported release is:

| Version | Security support |
|---|---|
| v1.1.1 | Supported |
| v1.1 and older | Not actively supported |

Users should move to the latest stable release before reporting an issue that may already have been corrected.

## Reporting a vulnerability

Please **do not publish vulnerability details, exploit steps, credentials, private network information, or proof-of-concept code in a public GitHub issue**.

Preferred reporting path:

1. Use GitHub's **Report a vulnerability** / private vulnerability reporting feature for this repository if it is available.
2. Include the affected Semaphore version, Windows version, reproduction conditions, security impact, and the minimum technical detail required to reproduce the problem.
3. Include logs or screenshots only after removing credentials, tokens, private addresses, personal information, and unrelated system data.

If private vulnerability reporting is not available, open a public issue containing **only a request to establish private security contact**. Do not include the vulnerability details in that issue.

## What to report

Security reports are especially relevant when they involve:

- unintended Windows Filtering Platform policy behavior;
- privilege-boundary or elevated-broker issues;
- unsafe loading or execution of privileged components;
- IPC authorization or trust-boundary problems;
- release/update integrity problems;
- parsing of untrusted blocklist/policy input that could cause code execution, privilege escalation, or persistent policy corruption;
- exposure of sensitive local information beyond Semaphore's intended functionality.

Ordinary bugs, UI defects, incorrect classifications, feature requests, and non-security crashes should use the normal issue tracker.

## Disclosure

Please allow reasonable time for investigation and a corrected stable release before public disclosure.

When a report is confirmed, the project will aim to:

- reproduce and assess the issue;
- determine affected versions;
- prepare and validate a fix;
- publish a corrected stable release when necessary;
- document security-relevant upgrade guidance.

## Release verification

Stable Semaphore releases publish the Windows executable together with `SHA256SUMS.txt`.

After downloading a release, the executable can be verified with PowerShell:

```powershell
Get-FileHash ".\Semaphore-v1.1.1-win-x64.exe" -Algorithm SHA256
```

Compare the resulting SHA-256 value with the checksum published in the same GitHub Release.
