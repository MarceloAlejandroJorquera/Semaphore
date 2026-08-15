# Semaphore

<p align="center">
  <img width="1734" height="782" alt="Screenshot_894" src="https://github.com/user-attachments/assets/deb3721c-0c18-40d3-a108-15ba90c0397a" />
</p>

<p align="center">
  <strong>Real-time Windows network visibility and firewall control.</strong>
</p>

<p align="center">
  Monitor live inbound, outbound and transit traffic, identify remote endpoints locally,
  and apply address, range, country, protocol, port and scoped network policy directly from the interface.
</p>

<p align="center">
  <a href="https://github.com/MarceloAlejandroJorquera/Semaphore/releases/latest"><img src="https://img.shields.io/badge/Release-v1.1.1-blue" alt="Release v1.1.1"></a>
  <a href="#whats-new-in-semaphore-v111"><img src="https://img.shields.io/badge/Status-Stable-brightgreen" alt="Stable"></a>
  <a href="#system-requirements"><img src="https://img.shields.io/badge/Platform-Windows%20x64-blue" alt="Windows x64"></a>
  <a href="#system-requirements"><img src="https://img.shields.io/badge/Qt-6.11.1-green" alt="Qt 6.11.1"></a>
  <a href="#native-windows-packet-capture"><img src="https://img.shields.io/badge/Capture-Windows%20Packet%20Monitor-blueviolet" alt="Windows Packet Monitor"></a>
  <a href="#windows-filtering-platform-firewall"><img src="https://img.shields.io/badge/Firewall-WFP-red" alt="Windows Filtering Platform"></a>
</p>

---

## Overview

**Semaphore** is a native Windows network monitoring and firewall-control application built for real-time traffic visibility and direct policy management.

It combines:

- live **Outbound**, **Inbound** and **Through** traffic monitoring;
- direct **Windows Filtering Platform (WFP)** enforcement;
- driverless capture through **Windows Packet Monitor**;
- IPv4 and IPv6 support;
- persistent Blacklist and Whitelist policy;
- country-level policy;
- Lane/direction, Protocol, Port and ID Filter scoping;
- local GeoIP, country-flag and ASN organization information;
- automatic endpoint identification without an online lookup service;
- repeated-address counters and per-event history;
- large blocklist/range management;
- release checking;
- system-tray operation;
- a compact Qt interface designed for high-rate traffic.

Semaphore is intended for users who want to see **where their system is communicating, what is communicating with it, and immediately control those connections** without installing a third-party packet-capture driver.

---

## What's new in Semaphore v1.1.1

**Semaphore v1.1.1 is the current stable release.**

v1.1.1 builds on the performance and large-list work delivered in v1.1 and substantially expands Semaphore's endpoint identification, policy model, WFP enforcement, blocked-traffic visibility and user interface.

### Major changes since v1.1

- Added **local ASN organization identification** for public IP addresses using packaged MaxMind ASN data.
- Added built-in identification for **well-known and special-purpose IPv4/IPv6 ranges**, including applicable multicast and local-scope traffic.
- Added deterministic endpoint-ID precedence: **manual ID/name → special-purpose identity → ASN organization → Unnamed**.
- Expanded Blacklist and Whitelist into a **unified policy model** capable of combining address/range, Lane/direction, Protocol, Port, Country and ID Filter constraints.
- Added individual protocol selection with separate IPv4/IPv6 protocol identities where applicable.
- Added explicit `Any` and `None` policy states; `None` is a disabled/non-matching condition rather than a wildcard.
- Added **multi-value ID Filters** with `*` and `?` wildcard support and OR semantics.
- Added policy normalization, duplicate collapse, compatible range merging and compatible Port-range coalescing.
- Added a complete **policy-summary hover** so composite rules can be inspected as badges without relying on a shortened generated ID.
- Improved Whitelist exception behavior and first-action unblock handling for historical blocked cells.
- Added **WFP classify-drop telemetry** so traffic successfully blocked before the normal capture path can still appear as a blocked event.
- Corrected blocked-event Outbound/Inbound direction classification.
- Hardened WFP reconciliation and removed stale effective-block state after successfully retired rules.
- Expanded traffic-history snapshots so historical rows preserve the policy state that existed when each event arrived.
- Expanded traffic iteration popups with the endpoint, port, flag, ID/name and protocol information relevant to each recorded event.
- Added compact badge rendering for policy values and monitor-table D&T / ID / Protocol values.
- Added complete-row viewport rendering so partially visible rows and country tiles are not painted.
- Added native Windows title-bar dragging, edge/corner resizing and improved Snap/maximize/restore behavior for the custom-framed window.
- Added a compact **settings cog** and production release checking.
- Improved startup restoration, generated-ID refresh, window placement, counter rendering, tooltips and numerous Qt 6.11.1 edge cases.

For the complete v1.1 → v1.1.1 development record, see **[CHANGELOG.md](CHANGELOG.md)**.

For security reporting and support policy, see **[SECURITY.md](SECURITY.md)**.

---

# Features

## Real-time network monitoring

Semaphore separates observed traffic into three live views:

### Outbound

Traffic originating from the local system and communicating with remote endpoints.

### Inbound

Traffic arriving at the local system from remote endpoints.

### Through

Forwarded, transit or otherwise non-local traffic observed by the capture backend.

Traffic tables can display information including:

- event sequence;
- date and time;
- origin and destination addresses;
- source and destination ports;
- protocol;
- country flag;
- endpoint ID/name;
- repeated-address counters;
- current allowed/blocked state.

Packet ingestion and accounting remain decoupled from Qt painting so high-rate traffic does not require one GUI event per packet.

---

## Native Windows packet capture

Semaphore uses the packet-monitoring facilities provided by Windows.

### No third-party capture driver required

Semaphore v1.1.1 does **not** require:

- Npcap;
- WinPcap;
- WinDivert;
- a Semaphore kernel capture driver;
- test-signing mode.

Privileged capture and firewall operations are isolated from the normal graphical interface and invoked only where Windows requires elevation.

---

## Windows Filtering Platform firewall

Semaphore applies active restrictions through the **Windows Filtering Platform (WFP)**.

The policy engine supports:

- individual IPv4 and IPv6 addresses;
- IPv4 and IPv6 ranges;
- CIDR networks;
- persistent Blacklist rules;
- Whitelist exceptions;
- country-derived coverage;
- Lane/direction scoping;
- Protocol constraints;
- Port constraints and compatible Port ranges;
- ID Filter constraints;
- live block/unblock operations;
- background policy reconciliation;
- safe policy retirement and purge.

Semaphore distinguishes **desired policy**, **confirmed effective WFP coverage** and the policy snapshot associated with recorded traffic.

### Blocked-traffic visibility

Semaphore's elevated broker can report classify-drop events produced by Semaphore-owned WFP filters.

That means a connection that is blocked before it reaches the ordinary packet-capture path can still be represented in the relevant traffic table as a blocked event.

---

## Unified policy model

Blacklist and Whitelist use one policy-table model rather than separate "absolute" and "scoped" pages.

A rule can combine applicable values from:

- **ID**
- **ID Filter**
- **Lane**
- **First IP Range**
- **Last IP Range**
- **Flag / Country**
- **Proto**
- **Port**

Simple address/range rules therefore remain simple, while more specific policy can be represented without creating a separate subsystem.

### Rule normalization

Semaphore normalizes policy created from the **Lists / policy** area, live traffic tables, history popups, startup restoration and rule editing.

Where policy scope is genuinely equivalent, Semaphore can:

- collapse exact duplicates;
- merge compatible address coverage;
- coalesce adjacent/overlapping Port ranges;
- merge compatible ID Filter sets.

Rules with materially different scope remain independent.

---

## Protocol and Port policy

Protocol selection exposes individual protocol identities rather than collapsing everything into broad groups.

Where applicable, address-family-specific identities remain distinct, for example:

- TCPv4 / TCPv6;
- UDPv4 / UDPv6.

Legacy generic protocol values are migrated according to the associated address family when possible.

Special selector values behave explicitly:

- **Any** — no constraint for that dimension;
- **None** — disabled/non-matching condition.

Port policy can target individual ports or compatible ranges. Adjacent/overlapping Port ranges coalesce only when every other policy dimension is equivalent.

---

## ID and ID Filter

### ID

The **ID** field is the human-readable identity associated with an endpoint or policy.

Manual IDs remain user-controlled.

For automatically generated identities, Semaphore can use local special-purpose and ASN information.

### ID Filter

**ID Filter** is a separate matching dimension.

It supports:

- `*` wildcard matching;
- `?` single-character wildcard matching;
- multiple simultaneous filter values;
- OR semantics between values;
- removable badge editing;
- compact scrolling for larger filter sets.

An empty ID Filter remains empty and does not become `Unnamed`.

---

## Automatic endpoint identification

Semaphore can identify many endpoints without an online address-lookup service.

### Naming/ID precedence

Automatic identity follows this precedence:

1. manually assigned ID/name;
2. recognized well-known or special-purpose identity;
3. ASN organization;
4. `Unnamed`.

Manual user values therefore remain authoritative.

### ASN organization lookup

Public addresses can be mapped to the organization associated with their autonomous system using a compact local ASN database generated from MaxMind GeoLite2 ASN data.

This can automatically identify organizations such as major network, cloud, CDN and service providers when the packaged ASN data contains the address.

### Special-purpose addressing

Semaphore also recognizes applicable well-known or special-purpose IPv4/IPv6 traffic so a generic ASN name is not used where a more useful local identity exists.

The classification covers applicable categories such as:

- multicast;
- link-local traffic;
- loopback/local addressing;
- well-known multicast services;
- scoped IPv6 multicast;
- other recognized special-purpose ranges.

Generated identities can be refreshed across tables when the canonical identity for an address changes.

---

## Direct traffic control

Blockable traffic cells can be acted upon directly.

Policy actions use the same normalized policy path as the **Lists / policy** area, so a block/unblock made from a traffic row or history popup does not create a separate incompatible rule format.

Whitelist exceptions are used when an endpoint must remain allowed while a broader deny policy still exists.

Historical traffic is not indiscriminately recolored by later policy changes; recorded policy state is retained per event.

---

## Repeated-address tracking

Repeated activity involving the same blockable endpoint can be condensed into a counter while retaining the underlying observations.

The counter display preserves the IP text, uses ordinary ellipsis when necessary and exposes the complete value through tooltips.

Double-clicking an eligible counter-bearing address opens a compact history popup.

Depending on the traffic direction, history rows can include:

- sequence number;
- date and time;
- remote endpoint;
- Port;
- Flag;
- ID/name;
- Protocol.

The history popup:

- is centered over Semaphore;
- displays a compact number of rows;
- scrolls when additional iterations exist;
- closes without adding a conventional application window.

---

## Blacklist

The Blacklist manages persistent deny policy.

Supported address inputs include:

- single IPv4 addresses;
- single IPv6 addresses;
- address ranges;
- CIDR networks;
- named ranges;
- imported blocklists;
- very large range collections.

The table also exposes the additional policy dimensions introduced in v1.1.1.

### Large-list handling

Semaphore retains the v1.1 large-policy architecture:

- unlimited Blacklist/Whitelist table presentation;
- numeric IPv4 range sorting and merging;
- batched table materialization and item reuse;
- dynamic `#` column sizing;
- progressive parse → optimize → materialize → save → WFP feedback;
- durable import checkpoints under `%LOCALAPPDATA%\Semaphore\blacklist\import-resume\`;
- restart recovery for interrupted work;
- preservation of the original imported source file;
- bounded WFP transactions;
- background reconciliation;
- priority for interactive policy changes;
- stale-operation invalidation;
- retry handling for transient failures;
- safe deletion and purge while reconciliation is active.

---

## Whitelist

Whitelist rules provide explicit Allow exceptions.

A Whitelist entry can remain effective inside broader Blacklist or Country policy according to the final normalized policy scope and WFP precedence rules.

Unblock actions from historical red traffic create the required exception on the first applicable action instead of requiring a second attempt.

---

## Country policy

Semaphore can derive network policy from its local GeoIP country data.

Country policy is expanded locally into the applicable address coverage and reconciled with the same effective policy system used by Blacklist and Whitelist.

### Country flags

Flags are rendered from vector resources while preserving native proportions, including unusually proportioned flags.

Country scrolling and resizing use complete tile rows so a final partial flag row is not painted at the viewport boundary.

---

## GeoIP and ASN information

Semaphore packages its geographic and network-organization data for local use.

Depending on the available information, Semaphore can use:

- country;
- city;
- country flag;
- ASN organization;
- special-purpose address classification.

GeoIP/ASN identification does not require a per-address remote lookup API.

---

## Traffic and policy table presentation

v1.1.1 adds a more compact visual language for structured values.

### Badges

Applicable values are rendered as content-sized badges, including:

- monitor-table D&T;
- monitor-table ID;
- monitor-table Protocol;
- policy ID Filter values;
- policy Protocol values;
- policy Port values;
- policy-summary hover values.

Through-table badge typography is slightly reduced where necessary so dense values remain inside the badge contour.

### Empty values

Applicable empty monitor/policy cells use a smooth diagonal marker.

The ID Filter field is intentionally excluded: an empty ID Filter remains visually blank.

### Tooltips

Long Blacklist/Whitelist address values expose their complete text when the displayed range is elided.

Composite policy IDs can expose the complete rule as badges on hover.

---

## Complete-row rendering and scrolling

Traffic and policy tables render only rows that fit completely inside the viewport.

- A partial bottom row remains hidden until its full height fits.
- A partial top row is not left painted during row-based scrolling.
- Mouse interaction follows complete visible rows.
- Vertical scrolling stays aligned to item/row increments.
- Country tiles follow the same complete-row principle.

This prevents clipped rows and half-visible flag tiles while resizing or scrolling.

---

## IPv4 and IPv6

Semaphore supports both IPv4 and IPv6 throughout its monitoring and policy workflows.

Supported input formats include:

```text
192.168.1.1
192.168.1.1-192.168.1.255
192.168.1.0/24

2001:db8::1
2001:db8::1-2001:db8::ffff
2001:db8::/64
```

Full and abbreviated IPv6 notation are supported where applicable.

---

# User interface

Semaphore v1.1.1 uses a compact custom-framed interface while retaining native Windows movement and resizing behavior.

Highlights include:

- custom centered Semaphore title bar;
- native title-bar drag/move behavior;
- resize handling from all four edges and corners;
- Windows Snap compatibility;
- maximize/restore behavior;
- persistent window placement;
- top-level settings cog;
- tab-based traffic navigation;
- color-coded policy state;
- content-sized badges;
- complete-row table rendering;
- native-style scrollbars;
- country flag layouts;
- compact traffic-history popups;
- system-tray integration.

The normal startup size remains larger than the minimum usable size, allowing the window to be resized down without disabling edge/corner resizing.

---

## Traffic state colors

Traffic and policy views distinguish current state visually.

Typical address states include:

- **Green** — allowed;
- **Red** — blocked.

Where partial/mixed policy state is shown, its calculation follows the same normalized policy precedence used by enforcement rather than treating every intersecting Allow rule as an override.

Historical traffic retains the state recorded for that event instead of being retroactively repainted solely because current policy changed later.

---

## Settings and release checking

The top-level settings cog provides compact application settings.

Semaphore can check the GitHub Releases feed for a newer stable version.

- Only a genuinely newer public release is presented as an update.
- Older public releases are not shown as updates to a newer running build.
- Version comparison supports Semaphore's variable-depth, zero-free release numbering.

---

# System tray

Semaphore can remain running through the Windows notification area.

The tray menu provides quick access to:

- **Open**
- **Atop**
- **Exit**

Window position, size and state are restored between sessions where applicable.

---

# Download

## Latest stable release: Semaphore v1.1.1

Download the latest binary from the:

**[Semaphore Releases page](https://github.com/MarceloAlejandroJorquera/Semaphore/releases/latest)**

Current Windows binary:

```text
Semaphore-v1.1.1-win-x64.exe
```

A SHA-256 checksum is provided alongside the release:

```text
SHA256SUMS.txt
```

---

# Installation

Semaphore v1.1.1 is distributed as a **portable Windows application**.

No traditional installer is required.

1. Download `Semaphore-v1.1.1-win-x64.exe` from the Releases page.
2. Place the executable in a directory of your choice.
3. Run Semaphore.
4. Approve Windows elevation when privileged capture or firewall operations require it.

### No Npcap installation is required.

---

# System requirements

| Requirement | Value |
|---|---|
| Operating system | Windows 10 / Windows 11 |
| Architecture | x64 |
| UI framework | Qt 6.11.1 |
| Packet capture | Windows Packet Monitor |
| Firewall backend | Windows Filtering Platform |
| Npcap | Not required |
| WinPcap | Not required |
| WinDivert | Not required |
| External Qt installation | Not required for the portable release |
| Administrator access | Required for privileged capture/firewall operations |

---

# Quick start

1. Launch Semaphore.
2. Approve the required Windows privilege elevation when requested.
3. Observe live traffic in **Outbound**, **Inbound** and **Through**.
4. Inspect Flag, ID and Protocol information for remote endpoints.
5. Open the **Lists / policy** tab (three-line glyph), then use **Blacklist** to create deny policy.
6. Use **Whitelist** in the same policy area for explicit exceptions.
7. Use Protocol, Port, Lane and ID Filter fields when a rule needs narrower scope.
8. Use **Country** in the policy area for country-derived policy.
9. Double-click an eligible repeated-address counter to inspect its individual events.
10. Use the settings cog for application settings and release checking.

---

# Blocklist formats

Semaphore supports common address and network formats.

### Single address

```text
192.168.1.1
```

### Address range

```text
192.168.1.1-192.168.1.255
```

### CIDR

```text
192.168.1.0/24
```

### Named range

```text
My Server|192.168.1.1-192.168.1.255
```

### IPv6

Equivalent IPv6 address, range and CIDR formats are supported.

---

# Architecture

Semaphore separates the ordinary GUI from privileged Windows networking operations.

```text
┌─────────────────────────────┐
│       Semaphore GUI         │
│     Qt / non-elevated       │
└──────────────┬──────────────┘
               │
               │ private IPC / privileged operations
               ▼
┌─────────────────────────────┐
│ Capture / Policy Component  │
└──────────────┬──────────────┘
               │
        ┌──────┴────────┐
        ▼               ▼
┌──────────────┐  ┌──────────────┐
│ Windows      │  │ Windows      │
│ Packet       │  │ Filtering    │
│ Monitor      │  │ Platform     │
└──────────────┘  └──────────────┘
```

The elevated component also reports relevant Semaphore-owned WFP drop telemetry back to the GUI so blocked events can remain observable.

---

# Privacy

Semaphore's monitoring, policy evaluation, GeoIP lookup, ASN organization lookup and special-purpose address identification are performed using local Windows/application resources.

Semaphore is not built around:

- a cloud account;
- remote network-management infrastructure;
- an online analytics dashboard;
- an external per-address GeoIP/ASN lookup API.

When release checking is enabled, Semaphore contacts the public GitHub Releases endpoint to determine whether a newer version is available. This is separate from traffic monitoring and endpoint identification.

---

# Scope

Semaphore is intended for:

- real-time endpoint traffic visibility;
- local connection monitoring;
- Windows firewall policy management;
- identifying unexpected network endpoints;
- address/range blocking;
- protocol/port-scoped policy;
- Blacklist management;
- Whitelist exceptions;
- country-level filtering;
- GeoIP/ASN-assisted traffic inspection;
- network troubleshooting.

Semaphore is **not** intended to replace a full:

- intrusion detection/prevention system;
- packet-analysis suite;
- VPN;
- router/firewall appliance;
- centralized enterprise security platform.

It is an endpoint-oriented monitoring and policy-control tool.

---

# Distribution and source availability

Semaphore v1.1.1 is currently distributed as a **compiled Windows binary**.

The source code is **not included with this release**. Source availability may change in the future.

Semaphore v1.1.1 is distributed under the terms of the MIT License. See [LICENSE](LICENSE) for details.

---

# Updating

To update a portable Semaphore installation:

1. Exit the currently running Semaphore instance.
2. Download the newer stable release.
3. Replace the previous executable.
4. Start Semaphore normally.

Persistent application data is maintained separately from the portable executable where applicable.

Semaphore uses **zero-free hierarchical version numbering**.

A component is written only when it is non-zero. Maintenance revisions extend the current version from `.1` through `.9`; after `.9`, the preceding component advances rather than introducing `.0`.

```text
v1
v1.1
v1.1.1
v1.1.1.1
v1.1.1.2
v1.1.1.3
v1.1.1.4
v1.1.1.5
v1.1.1.6
v1.1.1.7
v1.1.1.8
v1.1.1.9
v1.1.2
v1.1.2.1
v1.1.2.2
...
```

Zero components are omitted: for example, `v1.1.1` is used instead of `v1.1.1.0`.

---

# Security notes

Semaphore can modify active Windows network policy.

Blocking an incorrect:

- address;
- range;
- subnet;
- country;
- protocol;
- port;

can interrupt required network connectivity.

When applying broad policies, confirm that important infrastructure and management endpoints remain reachable.

Use Whitelist entries when explicit exceptions are required.

For vulnerability reporting, supported-version policy and disclosure guidance, see **[SECURITY.md](SECURITY.md)**.

---

# Support development

If you find Semaphore useful, you can support continued development:

[![PayPal](https://img.shields.io/badge/PayPal-Donate-blue)](https://www.paypal.com/paypalme/jorqueramarcelo)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Buy%20a%20Coffee-orange)](https://ko-fi.com/marcelojorquera)

---

# License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

The current public release is distributed in binary form; source code is not included with Semaphore v1.1.1.

---

# Acknowledgments

Semaphore is built using:

- **Qt**
- **Windows Packet Monitor**
- **Windows Filtering Platform**
- **MaxMind GeoLite2 City data**
- **MaxMind GeoLite2 ASN data**

Country flag artwork and other third-party resources are distributed according to their respective licenses and attribution requirements.

---

<p align="center">
  <strong>Semaphore v1.1.1</strong><br>
  Current stable release
</p>
