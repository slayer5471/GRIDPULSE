# GRIDPULSE — Smart Grid Monitoring and Energy Management

## Overview

GRIDPULSE is a proposed smart grid monitoring and energy management platform that explores how electrical circuit simulation, transformer monitoring, battery energy storage, and real-time visualization can work together.

The project is designed around an interactive electrical circuit editor, an engineering control center, and a FastAPI backend that connects the simulation with the monitoring interface. It also includes Solarex, a solar energy estimation platform, and a GRIDPULSE AI assistant for exploring system information.

**Project Status:** Concept demonstration and prototype representing our team's proposed plan and intended development direction.

This repository is intended to communicate our idea, system architecture, planned features, and technical approach. The presence of an interface or simulation feature does not necessarily mean that the corresponding functionality has been validated against real electrical equipment or deployed in a real power grid.

## Problem Statement

Electrical distribution networks require effective monitoring of transformer loading, energy consumption, renewable generation, and storage conditions. Limited visibility into these parameters can make it difficult to understand changing operating conditions and identify opportunities for better energy utilization.

GRIDPULSE proposes a software-based platform for visualizing electrical network behavior, exploring operating scenarios, monitoring system indicators, and investigating how battery energy storage could support energy management.

## Proposed Solution

GRIDPULSE combines three main components:

1. **Laptop A — Electrical Circuit Editor:** An interactive workspace for constructing electrical networks, configuring components, and exploring simulated power-flow conditions.
2. **Laptop B — Engineering Control Center:** A monitoring and analytics interface for viewing transformer status, battery information, alarms, energy flow, and engineering studies.
3. **FastAPI Backend:** A communication layer designed to exchange simulation telemetry, system state, and control commands between the applications.

The architecture separates the electrical simulation environment from the monitoring and control interface, making it possible to explore a two-computer deployment.

## Key Features

### Electrical Circuit Editor
- Interactive electrical circuit canvas.
- Electrical component configuration and network editing.
- Circuit topology validation.
- Power-flow visualization and power balance analysis.
- Scenario-based experimentation.
- What-If analysis and contingency studies.
- Anomaly detection and energy provenance exploration.

### Engineering Control Center
- Transformer loading and health indicators.
- Grid import and export monitoring.
- Battery Energy Storage System (BESS) monitoring.
- Power Conversion System (PCS) and PWM-related indicators.
- Electrical network and asset visualization.
- Alarms, events, and historical information.
- Energy analytics, forecasting views, and reports.
- Engineering studies and incident replay interfaces.

### Solarex
Solarex is the solar energy estimation component of the project. It is intended to help users explore potential solar installations using information such as location, electricity consumption, and available rooftop area.

Proposed outputs include solar panel requirements, estimated installation costs, potential savings, payback period, and environmental benefits. Actual estimates depend on the available inputs, assumptions, and data sources.

### GRIDPULSE AI
The project includes an AI assistant interface intended to support interaction with system information, monitoring data, and engineering insights. Its capabilities depend on the implemented backend integrations and available data.

## System Architecture

```text
┌─────────────────────────────┐
│ Laptop A                    │
│ Electrical Circuit Editor   │
│ Circuit and Simulation      │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ FastAPI Backend             │
│ Telemetry and System State  │
│ REST API and WebSocket      │
│ Control Command Routing     │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Laptop B                    │
│ Engineering Control Center  │
│ Monitoring and Analytics    │
│ Solarex and AI Interface    │
└─────────────────────────────┘
```

Laptop A is intended to provide the authoritative electrical simulation state. The backend exposes API endpoints and WebSocket telemetry, while Laptop B consumes the available data and sends supported control commands through the backend.

## Technology Stack

### Frontend
- React
- TypeScript
- Vite
- HTML and CSS
- Recharts
- React Leaflet and Leaflet

### Backend
- Python
- FastAPI
- Uvicorn
- REST APIs
- WebSockets

### Simulation and Analysis
- Custom electrical network modeling
- Pandapower integration
- OpenDSS integration
- Optional simulation adapters for additional tools

### Additional Components
- Solarex solar estimation interface
- GRIDPULSE AI assistant interface
- Engineering analytics and visualization
- Battery energy storage and power-flow representations

The availability and operational depth of individual integrations depend on the configured environment and implementation.

## Project Structure

```text
GRIDPULSE/
├── laptop-a/
│   └── Electrical Circuit Editor
├── laptop-b/
│   └── Engineering Control Center
├── backend/
│   ├── main.py
│   ├── engine.py
│   ├── high_fidelity.py
│   ├── simulation/
│   └── requirements.txt
├── legacy-combined-frontend/
├── run_backend.sh
├── run_backend.ps1
├── package.json
├── LAPTOP_A_README.md
├── LAPTOP_B_README.md
└── README.md
```

The `legacy-combined-frontend` directory contains an earlier frontend version and is not used by the current launch commands.

## Getting Started

### Prerequisites

Install the following tools:

- Node.js and npm
- Python 3.10 or a compatible version supported by the dependencies
- pip

### 1. Install Frontend Dependencies

From the project root:

```bash
npm install
```

### 2. Start Laptop A

```bash
npm run dev:laptop-a
```

Open:

`http://localhost:3001`

This launches the electrical circuit editor.

### 3. Start Laptop B

In another terminal, from the project root:

```bash
npm run dev
```

Open:

`http://localhost:3002`

This launches the engineering control center, Solarex, and the GRIDPULSE AI interface.

### 4. Start the Backend

On Linux or macOS:

```bash
./run_backend.sh
```

On Windows PowerShell:

```powershell
.\run_backend.ps1
```

The backend is intended to run on port `8000`. Its API documentation can be accessed at:

`http://localhost:8000/docs`

If running the backend manually, follow the setup instructions in `backend/README.md`.

## Two-Computer Setup

GRIDPULSE is structured to support a configuration in which Laptop A hosts the electrical simulation and backend, while Laptop B hosts the monitoring interface.

Configure the environment file for Laptop B using `laptop-b/.env.example` as a reference. Set the API and WebSocket URLs to the backend machine's reachable LAN address.

For example:

```text
VITE_API_URL=http://<BACKEND-LAN-IP>:8000
VITE_WS_URL=ws://<BACKEND-LAN-IP>:8000/ws/telemetry
```

Replace `<BACKEND-LAN-IP>` with the appropriate address of the machine running the backend. Both computers must be able to communicate over the network, and the required ports must be accessible.

## Testing and Build

Run the backend regression tests using:

```bash
PYTHONPATH=backend pytest -q backend
```

Build Laptop A:

```bash
npm run build:laptop-a
```

Build Laptop B:

```bash
npm run build:laptop-b
```

These commands support testing and building the project; successful execution and feature correctness should be verified in the target environment.

## Current Scope and Limitations

GRIDPULSE is being presented to demonstrate our team's concept, proposed architecture, and planned implementation of a software-based smart grid monitoring platform.

The repository contains frontend applications and backend simulation components, but it should not be interpreted as proof of a fully validated electrical digital twin or production-ready grid control system.

In particular:

- Simulation results require validation against appropriate electrical engineering models and reference data.
- Hardware integration and real transformer control are outside the scope of this conceptual demonstration unless separately implemented and validated.
- Forecasting, AI assistance, and advanced engineering analytics depend on the underlying data and implemented models.
- Real-world protection, switching, and grid control require appropriate safeguards, testing, and qualified engineering oversight.

## Future Development

Potential future work includes:

- Improving electrical simulation fidelity and validation.
- Integrating reliable telemetry with the engineering dashboard.
- Expanding transformer condition monitoring.
- Developing and evaluating forecasting models.
- Refining battery dispatch and energy management strategies.
- Improving anomaly detection and alarm handling.
- Exploring safe integration with real electrical equipment in a controlled environment.

## Intended Use

GRIDPULSE is intended for academic demonstration, concept development, engineering exploration, and future research planning. It is not intended to replace certified grid monitoring, protection, or control systems.

## Conclusion

GRIDPULSE represents our team's vision of combining electrical network simulation, transformer monitoring, energy storage, and intelligent software into a unified engineering platform.

This repository provides an initial representation of that vision, allowing others to understand our proposed architecture, planned features, and intended development direction.

It is a demonstration of our plan rather than a claim that every proposed capability has already been implemented or validated in real-world operating conditions.
