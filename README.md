# Market Data Ingestion & Time-Series Analytics Pipeline

A Python-based market data pipeline for ingesting, validating, storing, and analyzing time-series financial data using PostgreSQL and TimescaleDB.

## Overview

This project demonstrates a simple market-data ingestion workflow designed around reliability, data quality, time-series storage, and statistical analysis.

The pipeline:

- Fetches 5-minute OHLCV market data using Python
- Validates incoming data for missing values, duplicate timestamps, time gaps, invalid OHLC relationships, and volume issues
- Stores market data in PostgreSQL
- Uses TimescaleDB hypertables for time-series storage
- Implements duplicate-safe database insertion
- Includes retry logic with exponential backoff for API failures
- Demonstrates a failover mechanism for data-source failures
- Uses TimescaleDB time buckets for intraday aggregation
- Calculates VWAP, daily returns, volatility, and rolling volatility
- Uses z-scores to identify potential return anomalies
- Configures TimescaleDB columnstore for efficient historical data storage

## Architecture

Market Data API  
↓  
Python Ingestion  
↓  
Data Validation  
↓  
PostgreSQL + TimescaleDB  
↓  
Hypertable & Columnstore  
↓  
SQL Analytics  
↓  
VWAP / Returns / Volatility / Anomaly Detection

## Tech Stack

- **Python**
- **Pandas**
- **PostgreSQL**
- **TimescaleDB**
- **SQL**
- **psycopg2**
- **yfinance**
- **Jupyter / Google Colab**

## Key Concepts Demonstrated

### Data Ingestion
Market data is fetched programmatically and transformed into a structured format before being loaded into the database.

### Data Quality

The pipeline checks for:

- Missing values
- Duplicate timestamps
- Missing intraday intervals
- Invalid OHLC relationships
- Negative or zero volume
- Stale or incomplete observations

### Database & Time-Series Storage

PostgreSQL is used as the database layer, with TimescaleDB providing time-series functionality through hypertables, time-based chunking, time bucketing, and columnstore storage for historical data.

### Reliability

The ingestion process demonstrates:

- Retry logic
- Exponential backoff
- Failover handling
- Duplicate-safe insertion
- Basic missing-data detection and recovery concepts

### Statistical Analysis

The project calculates:

- VWAP
- Daily returns
- Historical volatility
- Rolling volatility
- Return z-scores
- Potential anomalies

## VWAP

Volume Weighted Average Price (VWAP) measures the average traded price weighted by trading volume.

\[
VWAP = \frac{\sum(Price \times Volume)}{\sum Volume}
\]

This provides a more volume-aware measure of the average price during a trading period.

## Project Structure

```text
market-data-ingestion-timescaledb/
│
├── market-data-ingestion-timescaledb.ipynb
└── README.md
