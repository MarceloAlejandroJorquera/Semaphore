# Semaphore

<p align="center">
  <img width="1672" height="780" alt="Screenshot_779" src="https://github.com/user-attachments/assets/deda3a98-56e4-49ae-ba40-8fe8b0e78707" />
</p>


<p align="center">
  <strong>Real-time Windows network visibility and firewall control.</strong>
</p>

<p align="center">
  Monitor live inbound, outbound and transit traffic, inspect its geographic origin,
  and apply IP, range or country-level network policy directly from the interface.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Release-v1-brightgreen" alt="Release v1">
  <img src="https://img.shields.io/badge/Status-Stable-brightgreen" alt="Stable">
  <img src="https://img.shields.io/badge/Platform-Windows%20x64-blue" alt="Windows x64">
  <img src="https://img.shields.io/badge/Qt-6.11.1-green" alt="Qt 6.11.1">
  <img src="https://img.shields.io/badge/Capture-Windows%20Packet%20Monitor-blueviolet" alt="Windows Packet Monitor">
  <img src="https://img.shields.io/badge/Firewall-WFP-red" alt="Windows Filtering Platform">
</p>

---

## Overview

**Semaphore** is a native Windows network monitoring and firewall-control application built for real-time connection visibility and direct policy management.

It combines:

- live Windows network traffic monitoring;
- direct Windows Filtering Platform enforcement;
- IPv4 and IPv6 support;
- persistent blacklists and whitelists;
- country-level network blocking;
- local GeoIP and country-flag information;
- address naming and repeated-address tracking;
- large blocklist and range management;
- system-tray operation;
- a compact, traffic-focused Qt interface.

Semaphore is designed for users who want to see **where their system is communicating, what is communicating with it, and immediately control those connections** without installing a third-party packet-capture driver.

---

## What's new in Semaphore v1

**Semaphore v1 is the first stable release of the current Semaphore architecture.**

Compared with the previous development versions, v1 introduces major changes throughout the capture, firewall, policy, GeoIP and user-interface layers.

### Major changes

- Replaced the previous Npcap capture architecture with **Windows Packet Monitor**.
- Replaced traditional Windows Firewall rule management with direct **Windows Filtering Platform (WFP)** enforcement.
- Added full **country-based blocking**.
- Added integrated **GeoIP city/country information and high-quality vector flags**.
- Added separate **Allowed** and **Blocked** country views.
- Added persistent **blacklist and whitelist** management.
- Added direct handling of individual addresses and IP ranges.
- Added scalable processing for **large blocklists**.
- Added repeated-address **iteration counters and history**.
- Improved IPv4 and IPv6 handling throughout the application.
- Redesigned the main interface, traffic tables, list views, system tray and detail popups.
- Added persistent window placement and improved tray restore behavior.
- Improved live policy-state reporting so displayed blocked state reflects active firewall policy more accurately.
- Added safer reconciliation and purge behavior for large policy sets.
- Removed the requirement for Npcap, WinPcap or WinDivert.

---

# Features

## Real-time network monitoring

Semaphore separates observed traffic into three live views:

### Outbound

Connections originating from the local system and communicating with remote endpoints.

### Inbound

Traffic arriving at the local system from remote endpoints.

### Through

Forwarded or transit traffic observed by the capture backend that is not represented as an ordinary local inbound or outbound connection.

Each traffic table can display information including:

- event sequence;
- date and time;
- origin address;
- destination address;
- source and destination ports;
- protocol;
- country flag;
- geographic information;
- saved address names;
- repeated-address counters;
- current allowed/blocked state.

Traffic information is updated continuously while monitoring is active.

---

## Native Windows packet capture

Semaphore uses the packet-monitoring facilities provided by Windows.

### No third-party capture driver required

Semaphore v1 does **not** require:

- Npcap;
- WinPcap;
- WinDivert;
- a Semaphore kernel capture driver;
- test-signing mode.

This substantially simplifies deployment compared with earlier Semaphore versions.

Privileged capture and firewall operations are isolated from the normal graphical interface and invoked only where Windows requires elevated privileges.

---

## Windows Filtering Platform firewall

Semaphore applies network restrictions directly through the **Windows Filtering Platform (WFP)**.

Supported policy operations include:

- blocking individual IPv4 addresses;
- blocking individual IPv6 addresses;
- blocking IPv4 and IPv6 ranges;
- persistent blacklist policies;
- whitelist exceptions;
- country-based policies;
- live block/unblock operations;
- policy reconciliation;
- policy purge.

This gives Semaphore direct control over active network filtering without depending on manually generated Windows Defender Firewall rules.

---

## Direct traffic control

Blockable address cells in the live traffic tables can be acted upon directly.

Semaphore distinguishes between:

- allowed traffic;
- blocked addresses;
- blacklist policy;
- whitelist exceptions;
- country policy;
- confirmed active WFP coverage.

This prevents historical traffic from being incorrectly recolored simply because a matching address or country was blocked later.

---

## Repeated-address tracking

Repeated network activity involving the same address can be condensed into a counter while retaining its individual observations.

For counter-bearing addresses, Semaphore stores the underlying iterations including applicable:

- sequence number;
- date and time;
- address;
- source/destination port information.

Double-clicking an eligible counter-bearing address opens a compact history popup.

The history viewer:

- has no conventional title bar;
- is centered over Semaphore;
- displays up to **7 rows** at once;
- automatically provides scrolling when more rows exist;
- closes by clicking outside the popup.

---

## Blacklist

The Blacklist view manages persistent network-deny policy.

Supported entries include:

- single IPv4 addresses;
- single IPv6 addresses;
- address ranges;
- CIDR networks;
- imported blocklists;
- large collections of ranges.

Semaphore automatically normalizes policy data and handles overlapping or adjacent ranges where appropriate.

### Large-list handling

The current policy engine is designed to remain responsive while processing large blocklists.

It includes:

- progressive policy application;
- bounded WFP transactions;
- background reconciliation;
- priority handling for interactive changes;
- stale-operation invalidation;
- retry handling for transient failures;
- safe deletion while reconciliation is active;
- safe purge behavior.

---

## Whitelist

The Whitelist provides explicit address exceptions.

Whitelisted endpoints can remain allowed even when broader blocking policy exists through a blacklist, range or country rule.

This allows a broad policy to remain intact while making selected exceptions without deleting the underlying source rule.

---

## Country blocking

Semaphore can control network policy geographically using its local GeoIP resources.

The **Country** view displays countries visually in two groups:

- **Allowed**
- **Blocked**

Clicking a country moves it between the two policy states.

Semaphore then translates that country policy into the applicable address coverage and reconciles it with the active Windows Filtering Platform configuration.

### Country flags

Country flags are rendered from high-quality vector resources.

Semaphore preserves native flag proportions rather than forcing every flag into a uniform aspect ratio, including unusually proportioned flags such as Qatar and Nepal.

---

## GeoIP information

Semaphore integrates local GeoIP information directly into the traffic interface.

Depending on the available data for an address, Semaphore can display:

- country;
- city;
- country flag.

Hover information provides geographic context without requiring a remote lookup service.

GeoIP resources are processed and packaged for efficient local use.

---

## Address naming

Frequently encountered addresses can be assigned a custom name.

Names:

- appear directly in the traffic tables;
- persist between sessions;
- remain independent from the current table contents;
- are not removed when traffic history is cleared.

This makes recurring infrastructure, servers and endpoints easier to identify at a glance.

---

## Traffic-table management

Each live traffic table includes a dedicated clear control.

Semaphore also provides a global clear control for:

- Outbound;
- Inbound;
- Through.

Clearing traffic resets the relevant visible history and sequence counters without deleting saved address names or firewall policy.

---

## IPv4 and IPv6

Semaphore supports both IPv4 and IPv6 throughout its primary monitoring and policy workflows.

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

# Screenshots

The screenshots below highlight the main Semaphore v1 workflows.

## Live Traffic

<!--
Upload the final Outbound / Inbound / Through screenshot to GitHub,
then replace this comment with:

<p align="center">
  <img width="1200" alt="Semaphore live traffic monitoring" src="YOUR-GITHUB-ASSET-URL" />
</p>
-->

Live Outbound, Inbound and Through traffic with ports, protocol, GeoIP information, flags, saved names and firewall state.

---

## Blacklist and Whitelist

<!--
<p align="center">
  <img width="1200" alt="Semaphore blacklist and whitelist management" src="YOUR-GITHUB-ASSET-URL" />
</p>
-->

Persistent address and range policies with direct Add, Delete, Delete Range and Purge controls.

---

## Country Blocking

<!--
<p align="center">
  <img width="1200" alt="Semaphore country blocking" src="YOUR-GITHUB-ASSET-URL" />
</p>
-->

Visual country-level policy management with separate Allowed and Blocked areas.

---

## Traffic Iteration History

<!--
<p align="center">
  <img width="900" alt="Semaphore traffic iteration history" src="YOUR-GITHUB-ASSET-URL" />
</p>
-->

Compact history views reveal the individual events represented by repeated-address counters.

---

# User interface

Semaphore v1 includes an extensively revised interface designed for dense network information while retaining normal Windows behavior.

Highlights include:

- custom Semaphore title bar;
- native Windows resize behavior;
- native maximize and restore;
- Windows Snap compatibility;
- persistent window placement;
- tab-based traffic navigation;
- color-coded traffic states;
- compact table controls;
- native table scroll behavior;
- country flag layouts;
- frameless traffic-history popups;
- system-tray integration.

---

## Traffic state colors

Traffic tables use immediate visual status indicators.

Typical address states include:

- **Green** — allowed;
- **Red** — blocked.

Visual state is tied to the relevant policy status rather than retroactively changing previous observations unnecessarily.

---

# System tray

Semaphore can remain running through the Windows notification area.

The tray menu provides quick access to:

- **Open**
- **Atop**
- **Exit**

Window size and position are remembered and restored between sessions.

Semaphore also uses Windows composition handling to reduce visible flashing during tray restore.

---

# Download

## Latest stable release: Semaphore v1

Download the latest binary from the:

**[Semaphore Releases page](https://github.com/MarceloAlejandroJorquera/Semaphore/releases/latest)**

Current Windows binary:

```text
Semaphore-v1-win-x64.exe
```

A SHA-256 checksum is provided alongside the release:

```text
SHA256SUMS.txt
```

---

# Installation

Semaphore v1 is distributed as a **portable Windows application**.

No traditional installer is required.

1. Download `Semaphore-v1-win-x64.exe` from the Releases page.
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
| Administrator access | Required only for privileged operations |

---

# Quick start

1. Launch Semaphore.
2. Allow the required Windows privilege elevation when requested.
3. Observe live traffic in **Outbound**, **Inbound** and **Through**.
4. Use the traffic address controls to block or allow an endpoint.
5. Use **Lists → Blacklist** to manage persistent blocked addresses and ranges.
6. Use **Lists → Whitelist** to manage explicit exceptions.
7. Use **Lists → Country** to allow or block traffic by country.
8. Minimize or close Semaphore to the system tray when appropriate.

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

Semaphore v1 separates its major responsibilities into distinct layers.

```text
┌─────────────────────────────┐
│       Semaphore GUI         │
│     Qt / non-elevated       │
└──────────────┬──────────────┘
               │
               │ privileged operations
               ▼
┌─────────────────────────────┐
│ Capture / Policy Component  │
└──────────────┬──────────────┘
               │
        ┌──────┴───────┐
        ▼              ▼
┌──────────────┐  ┌──────────────┐
│ Packet       │  │ Windows      │
│ Monitor      │  │ Filtering    │
│              │  │ Platform     │
└──────────────┘  └──────────────┘
```

This architecture keeps the primary interface non-elevated while isolating operations that require administrator privileges.

---

# Privacy

Semaphore performs its monitoring and firewall-management work locally.

The application is not built around:

- a cloud account;
- remote network-management infrastructure;
- an online analytics dashboard;
- an external GeoIP lookup API.

GeoIP information used by Semaphore is resolved from local application resources.

---

# Scope

Semaphore is intended for:

- real-time endpoint traffic visibility;
- local connection monitoring;
- firewall policy management;
- identifying unexpected network endpoints;
- IP and range blocking;
- blacklist management;
- whitelist management;
- country-level filtering;
- GeoIP-assisted traffic inspection;
- network troubleshooting.

Semaphore is **not** intended to replace a full:

- intrusion detection or prevention system;
- packet-analysis suite;
- VPN;
- router/firewall appliance;
- centralized enterprise security platform.

It is an endpoint-oriented monitoring and policy-control tool.

---

# Portable release and source availability

Semaphore v1 is currently distributed as a **compiled Windows binary**.

The source code is **not included with this release**.

Source availability may change in the future.

---

# Updating

To update a portable Semaphore installation:

1. Exit the currently running Semaphore instance.
2. Download the newer release.
3. Replace the previous executable.
4. Start Semaphore normally.

Persistent application data is maintained separately from the portable executable where applicable.

Semaphore uses compact version numbering:

```text
v1
v1.1
v1.1.1
v1.1.2
...
```

---

# Security notes

Semaphore can modify active Windows network policy.

Blocking an incorrect:

- address;
- range;
- subnet;
- country;

can interrupt required network connectivity.

When applying large policies, confirm that important infrastructure and management endpoints remain reachable.

Use whitelist entries when explicit exceptions are required.

---

# Support development

If you find Semaphore useful, you can support continued development:

[![PayPal](https://img.shields.io/badge/PayPal-Donate-blue)](https://www.paypal.com/paypalme/jorqueramarcelo)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Buy%20a%20Coffee-orange)](https://ko-fi.com/marcelojorquera)
[![Patreon](https://img.shields.io/badge/Patreon-Support-red)](https://www.patreon.com/c/MAJC)

---

# License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

The current public release is distributed in binary form; source code is not included with Semaphore v1.

---

# Acknowledgments

Semaphore is built using:

- **Qt**
- **Windows Packet Monitor**
- **Windows Filtering Platform**
- **MaxMind GeoIP data**

Country flag artwork and other third-party resources are distributed according to their respective licenses and attribution requirements.

---

<p align="center">
  <strong>Semaphore v1</strong><br>
  First stable release
</p>
