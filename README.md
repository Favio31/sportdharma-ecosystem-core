# SportDharma Ecosystem Core

> **Resilient Local-First Mesh Infrastructure for Offline Telemetry and Field Telecommunications**

`sportdharma-ecosystem-core` is an open-source (FOSS) software engine designed for extreme off-grid environments. Built with a 100% Local-First architecture, it ensures sovereign data handling, zero-cloud dependency, and high reliability in zero-connectivity mountainous or remote areas.

## Core Architectural Pillars

- **1. Map Engine (Offline GIS)**: Full offline vector map rendering utilizing `.pmtiles` formats based on OpenStreetMap (OSM) with embedded spatial indexing via local SQLite R-Tree and Geohash.
- **2. Chat Mesh (P2P Radio Transport)**: Dynamic multi-transport engine switching between BLE (Bluetooth Low Energy) for close proximity, Wi-Fi Direct, and LoRa mesh radio nodes (SX1262) for long-range valley/mountain communication.
- **3. Dharma Safe (Deterministic FSM Telemetry & SOS)**: Real-time telemetry processing running on deterministic Finite State Machines (FSM) inside isolated threads (`Dart Isolates`) for emergency dispatch and heartbeats.

## Compliance & Governance
- **License**: [Apache-2.0](LICENSE)
- **GenAI Transparency**: Strictly complies with NLnet GenAI Policy v1.1. Audit logs maintained in [PROMPT_PROVENANCE_LOG.md](PROMPT_PROVENANCE_LOG.md).
