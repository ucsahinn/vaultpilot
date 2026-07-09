# Executions Screen

The topbar `?` opens this page from the Executions screen. Use it to monitor active work such as updates, discovery runs, maintenance operations and background tasks.

## Work Here

- Check current status before retrying a job.
- Preserve error names, timestamps and component names for private support.
- Avoid repeated manual retries when a task is already running.

## Screen States

| State | Operator response |
| --- | --- |
| Running | Wait for the current job or cancel through the approved flow. |
| Failed | Keep error name, component and timestamp before retrying. |
| Stale | Check service health and related job screen before manual intervention. |

## Before You Act

- Check whether the job is still making progress before starting a replacement.
- Capture job ID, component, start time and last log summary for support.
- Avoid deleting job evidence while an update, discovery or maintenance incident is still under review.

## Safe Evidence

- Safe to share: job ID placeholder, component name, status, timestamp window and redacted error category.
- Keep private: local paths, hostnames, package download locations, raw logs, customer filenames and machine-specific traces.
- Preserve job evidence privately when update, discovery or maintenance work is still under review.

## Operator Notes

Execution details may include local paths, hosts, filenames or package state. Redact before sharing publicly.

## Related

- [Operator runbook](operator-runbook.md)
- [Update Center](update-center.md)
- [Discovery screen](screen-discovery.md)
