# ⚡ European Power Grid — Digital Twin

> A high-fidelity digital twin of the European interconnected transmission network, enabling real-time simulation, fault prediction, and grid stability analysis across the ENTSO-E synchronous area.

---

## 🗺️ Overview

This project builds a digital twin of the European high-voltage power grid, modelling the transmission infrastructure across the continental synchronous area (CE, Nordic, Baltic, and Great Britain zones).

It ingests real or synthetic SCADA telemetry, runs physics-based power flow solvers, and exposes the live grid state through an interactive map dashboard built with **Streamlit** and **Folium**.

The twin supports:

- **N-1 and N-k contingency analysis** — automatic detection of single or cascading line failures
- **Load forecasting** — ML-based demand prediction at the TSO and country level using LSTM + XGBoost
- **Renewable integration modelling** — variable generation from wind and solar assets
- **Market-coupled dispatch simulation** — merit-order dispatch and cross-border flows
- **Anomaly detection** — voltage, frequency, and topology deviations flagged in real time

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Data Ingestion Layer                  │
│      ENTSO-E Transparency API · SCADA · Weather APIs    │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                  Grid State Engine                      │
│   Power Flow Solver (Newton-Raphson) · State Estimator  │
│   Topology Processor · Contingency Engine · EMS Bridge  │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│               Analytics & ML Layer                      │
│     Load Forecast · Anomaly Detection · Stability       │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│             API & Visualisation Layer                   │
│      Streamlit Dashboard · Folium GIS Map · REST API    │
└─────────────────────────────────────────────────────────┘
```

---

## ✅ Features

| Module | Description | Status |
|--------|-------------|--------|
| Grid topology loader | Parses CGMES / CIM profiles for EU grid | ✅ Stable |
| AC power flow solver | Full Newton-Raphson, supports 5,000+ buses | ✅ Stable |
| DC approximation solver | Fast linearised flows for near-real-time use | ✅ Stable |
| State estimation | Weighted least-squares from pseudo-measurements | 🔄 In progress |
| N-1 contingency engine | Sequential line/transformer outage screening | ✅ Stable |
| Renewable dispatch model | Wind / solar probabilistic generation profiles | ✅ Stable |
| Load forecasting (ML) | LSTM + XGBoost ensemble per bidding zone | 🔄 In progress |
| Anomaly detection | Frequency / voltage deviation alerts | 🔄 In progress |
| Interactive map | Folium GIS map with live grid overlays | ✅ Stable |
| Streamlit dashboard | Real-time UI for monitoring and simulation | ✅ Stable |

---

## 🛠️ Tech Stack

| Layer | Tools |
|-------|-------|
| Language | Python |
| Data analysis | Pandas |
| Dashboard | Streamlit |
| Map visualisation | Folium, Streamlit-Folium |
| Machine learning | LSTM, XGBoost |
| Power flow solver | Newton-Raphson (custom implementation) |
| Data source | ENTSO-E Transparency API, SCADA feeds |
| Notebook environment | Jupyter Notebook |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/jussara08/Final.project.git
cd Final.project

# Install dependencies
pip install -r requirements.txt
```

### Run the dashboard

```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

---

## 📁 Project Structure

```
Final.project/
│
├── app.py                  # Streamlit dashboard entry point
├── requirements.txt        # Project dependencies
├── README.md
│
├── data copy/              # Processed datasets
├── raw/                    # Raw data from ENTSO-E and SCADA feeds
└── models/                 # Trained ML models (LSTM, XGBoost)
```

---

## 📊 Data Sources

- **ENTSO-E Transparency Platform** — European grid topology, load data, and generation forecasts
- **SCADA telemetry** — Real or synthetic operational grid measurements
- **Weather APIs** — Wind and solar irradiance data for renewable modelling

---

## 🔮 Roadmap

- [ ] Complete state estimation module
- [ ] Finish anomaly detection pipeline
- [ ] Deploy live dashboard to the web
- [ ] Add real-time ENTSO-E API integration
- [ ] Expand ML forecasting to all bidding zones

---

## 👩‍💻 Author

**Jussara Gaspar**
Data Scientist · Ironhack Bootcamp Graduate · Antwerp, Belgium

[![GitHub](https://img.shields.io/badge/GitHub-jussara08-181717?style=flat&logo=github)](https://github.com/jussara08)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
