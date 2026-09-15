# Technical Architecture & Module Design

> **SportDharma Ecosystem Core Engine**

This document specifies the software architecture, isolate boundaries, and local-first data pipelines for `sportdharma-ecosystem-core`.

---

## System Layering

┌─────────────────────────────────────────────────────────────────┐
│                    FLUTTER UI / USER LAYER                      │
└────────────────────────────────┬────────────────────────────────┘
│ Event Channel (Stream)
┌────────────────────────────────▼────────────────────────────────┐
│                   DART ISOLATE ENGINE (CORE)                    │
├─────────────────────────────────────────────────────────────────┤
│  • FSM Telemetry Engine (Deterministic State Handling)          │
│  • SQLite R-Tree Spatial Indexer (.pmtiles Vector Parser)       │
│  • Transport Layer Abstraction (BLE / Wi-Fi Direct / LoRa)     │
└─────────────────────────────────────────────────────────────────┘


## Core Modules Breakdown

### 1. Telemetry & FSM (`/lib/core/fsm`)
- Executed inside a dedicated **Dart Isolate** to prevent main-thread UI blocking during heavy sensor computation.
- Handles crash detection, static/immobility timers, and panic heartbeats.
- Outputs compact binary payloads for low-bandwidth radio dispatch.

### 2. Local Storage & Spatial Index (`/lib/core/storage`)
- **Database Engine**: Embedded SQLite with R-Tree spatial extensions and Geohash indexing.
- **Cartography**: Local parsing of `.pmtiles` vector files extracted from OpenStreetMap (OSM) data.
- **Zero-Cloud Guarantee**: All spatial queries are executed directly against the local storage layer without external network requests.

### 3. Abstract Radio Transport Layer (`/lib/core/radio`)
- Unified interface `RadioDriver` for physical link abstraction.
- **Transport Drivers**:
  - `BleTransportDriver`: Ad-hoc peer-to-peer local mesh (0–50 meters).
  - `WifiDirectTransportDriver`: High-bandwidth local data synchronization.
  - `LoraTransportDriver`: Long-range packet transmission via serial/BLE bridge to SX1262 nodes (868/923 MHz).

---

## Security & Privacy Rules
- **No Remote Telemetry**: User coordinates are never transmitted to centralized cloud servers.
- **Cryptographic Identity**: Ephemeral keypairs generated on-device for peer message authentication.
