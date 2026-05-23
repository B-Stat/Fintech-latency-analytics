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
    ROUND(AVG(CAST(latency AS REAL)), 2) AS average_latency_ms,
    ROUND(MAX(CAST(latency AS REAL)), 2) AS worst_latency_spike_ms
FROM network_dataset_labeled
GROUP BY hour_of_the_day
ORDER BY average_latency_ms DESC
LIMIT 5;
```
