# On-Chain Data Pipeline with LLM-Powered Daily Analysis

This project is an automated data engineering pipeline that fetches daily on-chain data from the Ethereum blockchain, calculates key performance metrics, and uses a Large Language Model (LLM) via Azure OpenAI to generate a daily intelligence report.
It demonstrates a modern ETL (Extract, Transform, Load) process, showcasing skills in concurrent data extraction, API integration, data transformation, and applying AI for automated analytical insights. The final output is a structured data file, ready for ingestion into a data warehouse or analytics platform.

## Key Features
- **Concurrent Data Extraction**: Utilizes a ThreadPoolExecutor to fetch block data in parallel, maximizing throughput while respecting API rate limits.
- **Automated Daily Reporting**: The script is designed to run without arguments, automatically processing data for a defined period (e.g., the last 24 hours).
- **LLM-Powered Insights**: Integrates with Azure OpenAI to move beyond simple metrics, generating qualitative, human-readable analysis and hypotheses about network activity.
- **Prompt Engineering**: Employs a sophisticated, persona-driven prompt to guide the LLM to act as a senior network analyst.
- **Analytics-Ready Output**: Saves the final data (quantitative metrics + qualitative summary) to a partitioned .csv file, a common format for data pipelines.
- **Secure & Configurable**: Manages API keys and configuration securely using environment variables (.env file).

## Tech Stack
- Language: Python 3.9+
- Data Processing: Pandas
- API Interaction: requests, concurrent.futures
- LLM Orchestration: LangChain
- LLM Provider: Azure OpenAI
- Configuration: python-dotenv

## Project Workflow
The pipeline follows a clear, automated ETL process:
```text
+--------------------------------+
| 1. Trigger Script              |
|    (e.g., daily schedule)      |
+--------------------------------+
             |
             v
+--------------------------------+
| 2. Extract On-Chain Data       |
|    - Fetch block range for day |
|    - Concurrently get all      |
|      transactions via Etherscan|
|      API (5 threads)           |
+--------------------------------+
             |
             v
+--------------------------------+
| 3. Transform & Aggregate       |
|    - Parse raw JSON data       |
|    - Calculate daily metrics   |
|      (tx count, avg gas, etc.) |
|      using Pandas              |
+--------------------------------+
             |
             v
+--------------------------------+
| 4. Generate LLM Insights       |
|    - Send metrics to Azure     |
|      OpenAI via LangChain      |
|    - Receive analytical summary|
+--------------------------------+
             |
             v
+--------------------------------+
| 5. Load Final Output           |
|    - Combine metrics & summary |
|    - Save to a date-partitioned|
|      CSV file (e.g., output/)  |
+--------------------------------+
```

## Prompt Engineering for Insight Generation
This project uses a specific prompt to guide the LLM to generate high-quality, structured analysis. The prompt assigns the LLM the persona of a senior analyst and asks it to perform a "deep dive" analysis rather than a simple summary.
- System Prompt: "You are a senior blockchain data analyst providing a daily intelligence report. You have deep knowledge of typical Ethereum network activity..."
- User Task: "Based on the metrics, provide your analysis in a structured format including an Executive Summary, Key Metric Analysis, and an Overall Hypothesis for the day's activity."

This approach demonstrates how LLMs can be integrated into a data pipeline not just to report data, but to create a new layer of automated, valuable insight.
