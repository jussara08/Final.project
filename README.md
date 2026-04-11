⭐️European Power Grid — Digital Twin

A high-fidelity digital twin of the European interconnected transmission network, enabling real-time simulation, fault prediction, and grid stability analysis across the ENTSO-E synchronous area.


Overview
This project builds a digital twin of the European high-voltage power grid, modelling the transmission infrastructure across the continental synchronous area (CE, Nordic, Baltic, and Great Britain zones). It ingests real or synthetic SCADA telemetry, runs physics-based power flow solvers, and exposes the live grid state through an API and interactive dashboard.
The twin supports:

N-1 and N-k contingency analysis — automatic detection of single or cascading line failures
Load forecasting — ML-based demand prediction at the TSO and country level
Renewable integration modelling — variable generation from wind and solar assets
Market-coupled dispatch simulation — merit-order dispatch and cross-border flows
Anomaly detection — voltage, frequency, and topology deviations flagged in real time


Architecture
┌─────────────────────────────────────────────────────────────────┐
│                        Data Ingestion Layer                     │
│   ENTSO-E Transparency API  ·  SCADA feeds  ·  Weather APIs     │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           
┌──────────────────────────▼──────────────────────────────────────┐
│                       Grid State Engine                         │
│    Power Flow Solver (Newton-Raphson)  ·  State Estimator       │
│    Topology Processor  ·  Contingency Engine  ·  EMS Bridge     │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           
┌──────────────────────────▼──────────────────────────────────────┐
│                     Analytics & ML Layer                        │
│    Load Forecast  ·  Anomaly Detection  ·  Stability Indices    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           
┌──────────────────────────▼──────────────────────────────────────┐
│                    API & Visualisation Layer                     │
│         REST / WebSocket API  ·  React Dashboard  ·  GIS Map    │
└─────────────────────────────────────────────────────────────────┘

Features
ModuleDescriptionStatusGrid topology loaderParses CGMES / CIM profiles for EU grid✅ Stable

AC power flow solverFull Newton-Raphson, supports 5 000+ buses✅ Stable

DC approximation solverFast linearised flows for near-real-time use✅ Stable

State estimationWeighted least-squares from pseudo-measurements🔄 In progress

N-1 contingency engineSequential line/transformer outage screening✅ Stable

Renewable dispatch modelWind / solar probabilistic generation profiles✅ Stable

Load forecasting (ML)LSTM + XGBoost ensemble per bidding zone🔄 In progress

Anomaly detectionFrequency / voltage deviation alerts🔄 In progress

REST APIOpenAPI 3.0 compliant grid state endpoints✅ Stable

WebSocket streamingLive telemetry push to dashboard clients✅ Stable

React dashboardInteractive map with grid overlays🔄 In progress
