# Threat Intelligence LLM Pipeline

This project implements an automated Threat Intelligence (CTI) pipeline that normalizes multi-source data, extracts high-value intelligence, and generates structured analyst-grade reports using LLMs and n8n.

The design prioritizes data fidelity, traceability, and strict control over hallucinations.

## Overview

The pipeline ingests heterogeneous Threat Intelligence sources (open-source, reports, feeds), merges them via n8n, and reduces them to a clean, high-signal JSON model suitable for Large Language Models.

The LLM is constrained to operate in strict analytical mode, producing professional Threat Intelligence reports without adding assumptions, enrichment, or external knowledge.

## Key Features

- Multi-source CTI ingestion and normalization  
- Extraction of high-value Threat Actor attributes only  
- MITRE ATT&CK normalization and deduplication  
- Explicit handling of actor names, aliases, and synonyms  
- Infrastructure and financial indicator extraction  
- Noise removal (crawler metadata, headers, telemetry)  
- LLM-ready JSON output with reduced token footprint  
- Strict anti-hallucination prompt design  

## Architecture

### 1. Data Ingestion
Multiple CTI sources are collected and merged using n8n.

### 2. Normalization and Extraction
A JavaScript Code node extracts only intelligence-relevant fields:
- Actor identity (name, aliases, synonyms)
- MITRE ATT&CK TTPs
- Tooling
- Infrastructure
- Financial indicators

### 3. LLM Processing
The cleaned JSON is passed to an LLM with a strict prompt that:
- Forbids inference or speculation
- Requires explicit JSON-backed statements
- Preserves analyst-grade tone and structure

### 4. Report Generation
The output is a structured Threat Intelligence report suitable for SOC, CTI, or executive consumption.

## Design Principles

- No enrichment beyond provided data  
- No inferred motivation, attribution, or intent  
- Every statement must be traceable to source JSON  
- Deterministic and auditable outputs  
- Separation of intelligence data from scraping telemetry  

## Intended Use Cases

- Threat actor profiling  
- SOC and CTI reporting  
- Intelligence summarization for executives  
- Input preparation for detection engineering or hunting  
- CTI automation workflows  

## Technologies Used

- n8n (workflow automation)  
- JavaScript (data normalization and extraction)  
- Large Language Models (report generation)  

## Status

This project is under active development and focused on reliability, correctness, and analyst trust rather than breadth or enrichment.

## Disclaimer

This project does not perform attribution, enrichment, or validation of Threat Intelligence data. The accuracy of outputs depends entirely on the quality and completeness of the input sources.
