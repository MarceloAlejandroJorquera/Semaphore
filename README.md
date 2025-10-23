# Semaphore

A modern, real-time network monitoring and firewall application built with Qt. Semaphore provides granular IP blocking with advanced range management capabilities.

![Platform](https://img.shields.io/badge/platform-Windows-blue)
![Qt](https://img.shields.io/badge/Qt-6.9.2-green)

## Features

### 🔍 Real-time Network Monitoring
- **Outbound Table**: Monitor connections your machine makes to other IPs
- **Inbound Table**: See IPs connecting to your machine
- **Through Table**: Monitor traffic that doesn't directly reach your machine (useful for troubleshooting)
- **Real-time logging** of all IP packets reaching your network interface

### 🛡️ Advanced Firewall Management
- **Granular IP Blocking**: Block individual IPs or entire ranges
- **IPv4 & IPv6 Support**: Full support for both IP versions
- **Range Optimization**: Automatic merging and splitting of IP ranges
- **Windows Firewall Integration**: Uses Windows Defender Firewall with Advanced Security
- **Persistent Rules**: Firewall rules persist after application closure

### ⚡ Smart User Interface
- **Hybrid Table System**: Last 10,000 rows displayed with pending rows system
- **Name Assignment**: Assign custom names to IP addresses
- **Visual Blocking Status**: Color-coded cells show blocked (red) and unblocked (green) IPs
- **System Tray Integration**: Minimal footprint with full functionality accessible via system tray

### 🔧 Advanced Features
- **CIDR Notation Support**: Import IP ranges using CIDR notation
- **Bulk Operations**: Process large blocklists with optimization
- **Duplicate Prevention**: Automatic detection and removal of duplicate ranges
- **Real-time Updates**: Live updates without interrupting user workflow

## Download

Get the latest installer from the [Releases page](https://github.com/MarceloAlejandroJorquera/Semaphore/releases/tag/v1.0.0).

## System Requirements

- **OS**: Windows 10/11 (64-bit)
- **Architecture**: x64
- **Dependencies**: Qt 6.9.2 runtime libraries included

## Quick Start

1. **Install**: Run the installer and follow the setup wizard
2. **Monitor**: Open Semaphore to see real-time network traffic
3. **Block IPs**: Double-click green cells in any table to block IPs
4. **Manage Rules**: Use the Blacklist tab to add, remove, or purge IP ranges

## Usage Guide

### Basic Blocking
- **Double-click** any IP cell to toggle blocking
- Blocked IPs appear in **red**, unblocked in **green**
- Names can be assigned to IPs for easy identification

### Advanced Range Management
- **Add Range**: Import blocklists in various formats (single IP, range, CIDR)
- **Remove Range**: Select and delete specific ranges
- **Purge All**: Completely clear all firewall rules and blocked IPs

### Table Navigation
- Scroll to the top to load pending rows
- Tab badges show pending row counts
- Names persist across sessions

## Blocklist Formats Supported

- **Single IP**: `192.168.1.1`
- **IP Range**: `192.168.1.1-192.168.1.255`
- **CIDR Notation**: `192.168.1.0/24`
- **Named Ranges**: `My Server|192.168.1.1-192.168.1.255`

## Building from Source

*Note: This is a binary-only release. Source code available for educational purposes.*

### Requirements
- Qt 6.9.2 (mingw_64)
- Windows 10/11 SDK
- C++17 compatible compiler

## Technical Details

- **Backend**: Windows Filtering Platform (WFP) integration
- **Frontend**: Qt 6.9.2 with custom table delegates
- **Performance**: Optimized for small to medium blacklists (thousands+ ranges)
- **Memory**: Efficient caching and lazy loading

## Support

If you find this software useful, consider supporting its development:

[![PayPal](https://img.shields.io/badge/PayPal-Donate-blue)](https://www.paypal.com/paypalme/jorqueramarcelo)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Buy%20a%20Coffee-orange)](https://ko-fi.com/marcelojorquera)
[![Patreon][https://www.patreon.com/posts/introducing-new-141909675?utm_medium=clipboard_copy&utm_source=copyLink&utm_campaign=postshare_creator&utm_content=join_link
](https://img.shields.io/badge/Patreon-Support-red)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with Qt Framework
- Uses Windows Defender Firewall with Advanced Security
