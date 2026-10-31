# Supabase Keep Alive

Automated GitHub Actions workflow that periodically pings Supabase REST API endpoints to keep projects active and verify database accessibility.

## Overview

This repository contains a scheduled GitHub Actions workflow that:

- Runs automatically on a schedule.
- Sends lightweight GET requests to Supabase tables exposed through the REST API.
- Verifies that the API is reachable using the project's anonymous key.
- Can be manually triggered from the GitHub Actions tab.

## Requirements

For each Supabase project:

- A publicly accessible table endpoint (through RLS policies or API permissions).
- A valid Supabase URL.
- A valid Supabase Anon Key.

## Repository Secrets

Configure the following GitHub Actions secrets:

### Project 1

| Secret | Description |
|----------|-------------|
| SUPABASE_URL_1 | Supabase project URL |
| SUPABASE_ANON_KEY_1 | Supabase anonymous key |

### Project 2

| Secret | Description |
|----------|-------------|
| SUPABASE_URL_2 | Supabase project URL |
| SUPABASE_ANON_KEY_2 | Supabase anonymous key |

## Workflow

The workflow runs on a scheduled basis and performs API calls such as:

```bash
GET /rest/v1/keepalive?select=id&limit=1
```

A successful response confirms the project is reachable and operational.

## Manual Execution

1. Open the **Actions** tab.
2. Select **Keep Supabase Alive**.
3. Click **Run workflow**.

## Notes

- Scheduled workflows execute from the repository's default branch.
- GitHub may delay cron jobs during periods of high load.
- The workflow is intentionally lightweight and generates minimal database activity.
- Repository secrets are never exposed in workflow logs.

## License

MIT
