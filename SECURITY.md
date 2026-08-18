# Security Policy

## Supported Versions

Security fixes are provided for the current stable Semaphore release.

| Version | Supported |
|---|---|
| `v1.1.1.2` | Yes |
| `v1.1.1.1` | No |
| `v1.1.1` | No |
| `v1.1` | No |
| `v1` | No |
| Pre-release / development builds | No |

Older releases may remain available for archival purposes, but users should move to the current stable release when practical.

## Reporting a Vulnerability

Please **do not open a public GitHub Issue** for a vulnerability that could put users or networks at risk.

If private vulnerability reporting is enabled for the repository, use GitHub's private security reporting feature from the repository's **Security** area. Include enough information to reproduce and assess the issue safely.

Useful report details include:

- affected Semaphore version;
- Windows version and architecture;
- clear reproduction steps;
- whether administrator elevation is required;
- whether the issue can be triggered by local or remote network traffic;
- the relevant address/range, Lane, Protocol, Port, Country or ID Filter policy scope when applicable;
- whether Windows Packet Monitor capture, WFP enforcement, the elevated broker, persistence, GeoIP/ASN processing or release checking is involved;
- sanitized logs, screenshots or crash information;
- the security impact you believe is possible.

Do not include credentials, private keys, unrelated personal information, or sensitive network data that is not needed to reproduce the issue.

## Security-Relevant Areas

Examples of issues that should be reported privately include:

- local privilege escalation or an unintended elevation boundary bypass;
- unsafe broker/GUI IPC handling;
- WFP policy that can be bypassed when Semaphore reports it as enforced;
- unintended traffic blocking/allowing caused by malformed or corrupted persistent policy state;
- memory-safety or denial-of-service conditions caused by untrusted network/capture data;
- unsafe parsing of imported blocklists, ranges, CIDR data or generated GeoIP/ASN resources;
- arbitrary file creation, overwrite or path traversal in persistence/import/update tooling;
- integrity failures in generated portable payloads or release assets;
- sensitive-data disclosure beyond normal network-monitoring visibility;
- vulnerabilities in bundled dependencies that materially affect Semaphore.

Ordinary UI defects, performance problems, incorrect non-security presentation and feature requests should normally use regular GitHub Issues unless they also create a security impact.

## Coordinated Disclosure

Please allow reasonable time for investigation and remediation before public disclosure. Additional information or a reproducible test case may be requested before an issue can be confirmed.

Security fixes may be released using Semaphore's compact zero-free hierarchy, for example:

```text
v1.1.1
v1.1.1.1
v1.1.1.2
v1.1.1.3
...
v1.1.2
```

Published binaries should be accompanied by SHA-256 checksums so users can verify the exact downloaded assets.

## Binary Distribution

Semaphore stable releases are distributed as portable Windows x64 assets. The public release may be binary-only. Security reports remain in scope for the released binary, privileged broker behavior, policy/persistence formats, generated resources and network behavior regardless of source availability.

## Network and Privacy Notes

Semaphore monitors local network activity and can actively modify Windows Filtering Platform policy. GeoIP, ASN organization and special-purpose address identification are performed from local application resources. When release checking is enabled, Semaphore contacts the public GitHub Releases API after startup and approximately hourly while running to determine whether a newer stable release exists. This release check does not upload captured traffic, firewall Rules, endpoint history, GeoIP/ASN results or usage analytics.

## Responsible Testing

Only test systems, networks and policy environments that you own or are authorized to test. Avoid experiments that could disrupt third-party systems or unrelated network users.
