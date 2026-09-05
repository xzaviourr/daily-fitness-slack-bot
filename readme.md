# Daily Fitness Challenge Slack Bot

A Flask-based Slack app that posts daily movement challenges, sends reminder
nudges, and records completion interactions in PostgreSQL. The project was
designed as an AWS Elastic Beanstalk deployment with cron-driven helper scripts.

> **Historical project:** this repository is archived and is not maintained.
> It uses a 2022-era Slack API contract and dependency set.

## Features

- Slack Events API endpoint for mentions, messages, and reactions
- interactive-action endpoint for completion buttons
- scheduled morning challenge and reminder scripts
- Slack Block Kit message generation
- PostgreSQL challenge and completion records
- Flask application entry point compatible with Elastic Beanstalk conventions

## Setup

Use a Python version compatible with the pinned dependencies (Python 3.8 is a
reasonable starting point):

```bash
git clone https://github.com/xzaviourr/daily-fitness-slack-bot.git
cd daily-fitness-slack-bot
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python application.py
```

Before launch:

1. Create a Slack app and configure its Events API and interactivity URLs.
2. Supply a bot OAuth token and endpoint configuration in
   `config/credentials.json`.
3. Configure a PostgreSQL database in `config/db_credentials.json`.
4. Apply the schema expected by `database/db_queries.yaml`.

The checked-in JSON files are templates. Never commit real Slack tokens or
database passwords. Use a secret manager or deployment environment for any
revival.

The Flask server listens on port 8080 when run directly. The cron scripts are
separate processes and are not started by `application.py`.

## API behavior

- `GET /` — health text
- `POST /interactivity/` — completion button callbacks
- `POST /event/` — Slack URL verification and selected event callbacks

## Limitations

- Slack request signatures are not verified.
- SQL strings and incoming payloads need additional validation.
- There is no automated schema migration or meaningful test suite.
- Fitness prompts are general engagement content, not medical or exercise
  advice. Users should adapt activity to their abilities and professional
  guidance.

## Maintenance and license

This repository is preserved as a historical collaborative project. No license
is asserted because authorship is shared.
