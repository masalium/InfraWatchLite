# InfraWatchLite

InfraWatchLite is a small Linux system monitoring utility that periodically records basic resource usage and emits warnings when predefined thresholds are exceeded.

The tool is intended for lightweight observability on single machines where full monitoring stacks are unnecessary.

---

## Overview

InfraWatchLite samples system metrics at a fixed interval and writes them to a log file.
It focuses on visibility and traceability, not dashboards or long-term analytics.

---

## What it does

- Samples CPU usage
- Samples memory usage
- Samples disk usage
- Writes timestamped records to a log file
- Emits warnings when configured thresholds are crossed

---

## Inputs

- System resource metrics provided by the host OS
- Configuration values defined in `config.json`

---

## Outputs

- `logs/monitor.log`  
  Plain-text log containing timestamped resource usage and warning messages.

---

## How to run

### Install dependencies
```bash
pip install -r requirements.txt
```

### Run
```bash
python3 infrawatchlite.py
```

Logs will be written to:
```text
logs/monitor.log
```

---

## Configuration

Thresholds and sampling interval are defined in `config.json`.

Configurable values include:
- CPU usage threshold
- Memory usage threshold
- Disk usage threshold
- Monitoring interval (seconds)

Changes take effect on the next run.

---

## Example log output (shape)

```text
2025-02-01 14:03:12 CPU=42% MEM=61% DISK=73%
2025-02-01 14:03:42 CPU=88% MEM=64% DISK=73% WARNING: CPU threshold exceeded
```

---

## Design notes

InfraWatchLite is intentionally minimal. It relies on periodic sampling and file-based logging to keep behavior transparent and easy to audit. The goal is to provide a clear record of system conditions over time without introducing external services or complex dependencies.

---

## Limitations

- Designed for single-host monitoring
- No alerting beyond log warnings
- No persistence beyond log files
- Not intended as a replacement for full monitoring stacks

---

## Executable version (future)

This project can be packaged as a standalone executable for environments where Python is not available. When provided, the executable will preserve the same configuration and logging behavior.
