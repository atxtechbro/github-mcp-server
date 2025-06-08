# Enhancement: Efficient Failed Job Logs

## Problem
Getting failed job logs requires either downloading ALL logs (inefficient) or manual multi-step process.

## Solution
Enhance `get_job_logs` with:
- `run_id` + `failed_only=true` - Gets only failed job logs
- `return_content=true` - Returns actual log content vs URLs

## Benefits
- Token efficient (like `gh run view --log-failed`)
- Backward compatible
- Eliminates additional HTTP requests

## Usage
```bash
# Current: Single job
get_job_logs --job_id=12345

# New: All failed jobs with content
get_job_logs --run_id=67890 --failed_only=true --return_content=true
```
