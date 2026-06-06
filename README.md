# Phira Chart Auto Downloader

This project automatically fetches the latest chart metadata and chart JSON files from the Phira API and stores them in this repository.

## Features

- Automatically fetches latest chart IDs from:
    https://api.phira.cn/chart?page=1&order=-updated  
- Downloads full chart JSON data from:
    https://api.phira.cn/chart/{chart_id}  
- Saves data to:
    /chart/info/{chart_id}.json  
- Automatically overwrites outdated files
- Runs daily via GitHub Actions
- Only commits changed files to reduce noise

## File Structure

chart/   info/     123.json     124.json     ... .github/   workflows/     fetch_phira.yml

## How It Works

1. GitHub Actions runs daily (or manually via workflow_dispatch)
2. Fetches latest chart list sorted by update time
3. Extracts all chart IDs from results
4. Downloads each chart's full JSON data
5. Saves it locally in chart/info/
6. Commits and pushes updates automatically

## Manual Run

You can manually trigger the workflow:

GitHub Repository → Actions → Update Phira Charts → Run workflow

## Requirements

- GitHub Actions enabled
- Write permission enabled for workflow

## Notes

- API may occasionally timeout; retries are handled in workflow
- Only the latest page is fetched by default
- Designed for lightweight incremental syncing

## License

You may use and modify this project freely.

---
<iframe src="https://example.com" width="600" height="400"></iframe>
