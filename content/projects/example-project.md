+++
title = 'Example Data Platform Migration'
date = 2025-11-03
summary = 'Migrated a legacy Ruby ETL pipeline to a Python and Airflow platform, cutting nightly batch runtime from six hours to under ninety minutes.'
stack = ['Python', 'Airflow', 'PostgreSQL', 'dbt', 'AWS Glue']
role = 'Lead Data Engineer'
dates = 'Feb 2025 – Jun 2025'
series = ['platform-rebuild']
draft = false

[links]
repo = 'https://example.com/repo/example-project'
writeup = 'https://example.com/writeup/example-project'
+++

## Background

The nightly batch pipeline had grown organically over several years as a set of
Ruby scripts kicked off by cron. Each new data source added another script,
another cron entry, and another set of undocumented assumptions about run
order. By early 2025 a full run took six hours and a single failed step
required a manual restart of the whole chain.

## Approach

The rebuild moved orchestration to Airflow and reimplemented each extraction
and transformation step in Python, backed by dbt models for the warehouse
layer. Sources were migrated incrementally behind a shared interface so the
old and new pipelines could run in parallel and be diffed against each other
before the legacy scripts were retired.

Key decisions:

- Idempotent tasks throughout, so any DAG run could be safely retried.
- Row counts logged at each transformation step for auditability.
- AWS Glue jobs for the two largest, most compute-heavy extracts.

## Results

The full run now completes in under ninety minutes, with per-source retries
instead of whole-pipeline restarts. Row-count logging at each step also
surfaced two long-standing data quality issues in the original Ruby scripts
that had been silently dropping rows on malformed input.
