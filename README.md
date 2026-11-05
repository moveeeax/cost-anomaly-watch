# cost-anomaly-watch

> Tells you the bill jumped. Once.

**Status:** 🚧 In development

## Overview

Detect day-over-day cost anomalies per service against a rolling baseline and alert once per anomaly, not once per run.

## Features

- Builds a rolling baseline per service, region and account, with weekday and weekend seasonality kept apart
- Scores each day by deviation from the baseline and by absolute dollars, so a 400% jump on a $2 service stays quiet
- Deduplicates alerts by anomaly fingerprint in a state store, so a cron every hour does not page six times for one spike
- Resolves an anomaly and posts a closing message when spend returns to baseline
- Slack alerts with the offending service, the delta, and the last seven days as a sparkline
- Dry-run mode that prints what would have fired over a historical window, for tuning thresholds before you turn it on

## Stack

Python + boto3, click, slack-sdk, pandas for the baseline, and SQLite for alert state.

## Usage

```bash
cost-anomaly-watch --baseline-days 30 --threshold 2.5-sigma --min-delta 50 \
  --slack-channel '#finops-alerts' --state ./anomalies.db
```

## License

MIT

---

Archived on 2026-11-05. The idea moved to [aws-cost-slack](https://github.com/moveeeax/aws-cost-slack/issues/2).
