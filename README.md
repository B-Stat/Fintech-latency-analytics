# Fintech Infrastructure Latency Analytics

## Project Overview
This project models and analyzes real-world network traffic logs to evaluate routing stability and identify high-frequency latency spikes. 

## Key Technical Achievements
- Structured an automated CSV ingestion framework inside an optimized relational database engine.
- Designed time-series queries to parse timestamps and group analytical logs into precise hourly blocks.
- Calculated rolling operational metrics to pinpoint severe infrastructure congestion points.

## Core Analytics Code
```sql
SELECT 
    SUBSTR(timestamp, 1, 13) || ':00:00' AS hour_of_the_day,
    COUNT(*) AS total_network_requests,
    ROUND(AVG(CAST(latency AS REAL)), 2) AS average_latency,
    ROUND(MAX(CAST(latency AS REAL)), 2) AS worst_latency_spike
FROM network_dataset_labeled
GROUP BY hour_of_the_day
ORDER BY average_latency DESC
LIMIT 5;
```

## Core Analytical Findings


| Analysis Scope / Windows | Total Network Requests | Average Latency | Peak Volatility Spike | Fintech Risk Analytics & Operational Impact |
| :--- | :---: | :---: | :---: | :--- |
| **Full Dataset Baseline Summary** | **1,001** | **54.76 ms** | **3,051.58 ms** | Establishes project scale; flags a 3+ second extreme system delay anomaly. |
| **Peak Window (15:00:00)** | 76 | 153.66 ms | 3,049.50 ms | Highest sustained baseline delay; requires alternate infrastructure routing. |
| **Peak Window (16:00:00)** | 67 | 97.81 ms | 3,031.66 ms | High sustained volatility; network capacity severely degraded. |
| **Peak Window (17:00:00)** | 90 | 73.09 ms | 1,034.97 ms | Maximum request volume window; testing localized server capacity boundaries. |
| **Peak Window (18:00:00)** | 87 | 124.05 ms | 3,051.58 ms | Absolute worst absolute traffic spike encountered; high transaction timeout risk. |
| **Peak Window (22:00:00)** | 93 | 65.03 ms | 1,043.53 ms | Elevated baseline noise; points to secondary scheduled data-load congestion. |

### 📈 Infrastructure Latency Variance Flow
```mermaid
graph TD
    %% Define the core dataset overview
    A[<b>Full Dataset Base Summary</b><br>1,001 Total Log Requests<br>Global Baseline Avg: 54.76ms] --> B(Isolated Peak Latency Outliers)

    %% Link the top 5 high-volatility outlier hours chronologically
    B --> C[Hour 15:00<br>76 Requests<br>Avg: 153.66ms<br>Max Spike: 3,049.5ms]
    B --> E[Hour 16:00<br>67 Requests<br>Avg: 97.81ms<br>Max Spike: 3,031.66ms]
    B --> F[Hour 17:00<br>90 Requests<br>Avg: 73.09ms<br>Max Spike: 1,034.97ms]
    B --> D[Hour 18:00<br>87 Requests<br>Avg: 124.05ms<br>Max Spike: 3,051.58ms]
    B --> G[Hour 22:00<br>93 Requests<br>Avg: 65.03ms<br>Max Spike: 1,043.53ms]

    %% Operational risk-level warning styles
    style C fill:#ffcccb,stroke:#b22222,stroke-width:2px;
    style E fill:#ffcccb,stroke:#b22222,stroke-width:2px;
    style F fill:#ffe5b4,stroke:#d2691e,stroke-width:1px;
    style D fill:#ffcccb,stroke:#b22222,stroke-width:2px;
    style G fill:#ffe5b4,stroke:#d2691e,stroke-width:1px;

