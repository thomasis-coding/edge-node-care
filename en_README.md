# Edge Node Care

> Local edge computing node on Raspberry Pi for automatic network failover — Academic Proof of Concept (ECE Paris, 2nd year)

---

## Context

This project explores a **local fallback solution (Edge Computing)** capable of maintaining access to critical data during a network outage. The theoretical use case targets the healthcare sector, where continuous data access can be vital.

This is a **functional prototype**, not a production-ready system.

---

## Architecture

The system relies on automated failover between two environments:

**Nominal mode** — the Raspberry Pi continuously syncs data in the background from the VPS.

**Emergency mode** — the Watchdog script detects the loss of cloud connectivity and:
1. Forces the Raspberry Pi to broadcast its own local Wi-Fi hotspot
2. Deploys an emergency web interface (codenamed "Ambre") accessible from that network

---

## Tech stack

| Component | Technology |
|---|---|
| Local node | Raspberry Pi (Debian) |
| Fallback API | Python · FastAPI |
| Failure detection | Python Watchdog script |
| Networking | `nmcli` · Linux network interface management |
| Processes | Linux background services |

---

## Key learnings

This project was an opportunity to go beyond pure coding and understand how software interacts with hardware and networks:

- **Linux/Debian sysadmin** : TCP port management, network interface manipulation (`nmcli`), background process lifecycle
- **API design** : building a REST API with FastAPI
- **AI-assisted development** : using LLMs as a technical unblocking tool for networking and system configuration challenges

---

## Known limitations

This 2nd-year prototype successfully validates the emergency failover but has identified limitations:

- **Incomplete resilience loop** : detecting the return of internet connectivity and syncing back to the main server after a crisis requires manual intervention
- **System permission handling** : network failover scripts occasionally conflict with OS security (`sudo`), making full automation not viable without dedicated configuration

---
