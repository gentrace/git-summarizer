# Git Weekly Summary Action

A GitHub Action that generates weekly summaries of code changes using OpenAI and sends them to Slack.

## Features

- Analyzes git commits over a specified time period
- Uses OpenAI's models to generate human-readable summaries
- Posts summaries directly to a Slack channel
- Configurable analysis period and model selection

## Usage

Add this action to your GitHub workflow:

```yaml
name: Weekly Code Summary
on:
  schedule:
    - cron: "0 10 * * 1" # Runs at 10:00 AM every Monday
  workflow_dispatch: # Allows manual triggering

jobs:
  summarize:
    runs-on: ubuntu-latest
    steps:
      - uses: gentrace/git-summarizer@v1
        with:
          openai_api_key: ${{ secrets.OPENAI_API_KEY }}
          slack_bot_token: ${{ secrets.SLACK_BOT_TOKEN }}
          slack_channel: "engineering" # Required - channel to post to
          days_to_analyze: "7" # Optional, defaults to 7
          model: "o1" # Optional, defaults to o1
```

## Inputs

| Input             | Description                             | Required | Default |
| ----------------- | --------------------------------------- | -------- | ------- |
| `openai_api_key`  | OpenAI API key for generating summaries | Yes      | -       |
| `slack_bot_token` | Slack Bot Token for sending messages    | Yes      | -       |
| `slack_channel`   | Slack channel to post the summary to    | Yes      | -       |
| `days_to_analyze` | Number of days of history to analyze    | No       | 7       |
| `model`           | OpenAI model to use for summarization   | No       | o1      |

## Setup

1. Create an OpenAI API key at https://platform.openai.com
2. Create a Slack Bot Token at https://api.slack.com/apps
3. Add both tokens as secrets in your GitHub repository
4. Add the workflow file to your repository at `.github/workflows/weekly-summary.yml`
5. Make sure your Slack bot has been invited to the target channel

## License

MIT
