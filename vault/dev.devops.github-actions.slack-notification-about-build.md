---
id: 51azscfri4ryi1qpwh4s0nq
title: Github action - Slack notification about build
desc: ""
updated: 1685950374564
created: 1685948804057
---

```yml
# Build.yml
name: "[main] build, deploy"
env:
  SLACK_CHANNEL_ID: ${{ SLACK_CHANNEL_ID }}
  SLACK_BOT_TOKEN: ${{ secrets.SLACK_NOTIFICATIONS_BOT_TOKEN }}
  # https://api.slack.com/reference/messaging/payload
  # https://github.com/orgs/community/discussions/27058#discussioncomment-3254475
  ATTACHMENTS_AUTHOR: |
    "author_name": "${{github.event.sender.login}}",
    "author_link": "${{github.event.sender.html_url}}",
    "author_icon": "${{github.event.sender.avatar_url}}"
  PAYLOAD_BLOCKS: |
    "blocks": [
      {
        "type": "header",
        "text": {
          "type": "plain_text",
          "text": "🈺 [Project name]"
        }
      },
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": ${{ toJSON(github.event.head_commit.message) }} # multiline
        }
      },
      {
        "type": "actions",
        "elements": [
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "🌏 Site"
            },
            "url": "https://www.project.com/"
          },
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "📝 Commit link"
            },
            "url": "${{ github.event.head_commit.url }}"
          },
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "⚙️ Action log"
            },
            "url": "https://github.com/${{ github.repository }}/actions/runs/${{ github.run_id }}"
          }
        ]
      }
    ]
on:
  workflow_dispatch:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 4
    strategy:
      matrix:
        node-version: [18.x]
    permissions:
      id-token: write
      contents: read
    steps:
      - name: Notify start to slack
        id: slack
        uses: slackapi/slack-github-action@v1
        with:
          channel-id: ${{env.SLACK_CHANNEL_ID}}
          payload: |
            {
              ${{env.PAYLOAD_BLOCKS}},
              "attachments": [
                {
                  ${{ env.ATTACHMENTS_AUTHOR }},
                  "color": "dbab09",
                  "fields": [
                    {
                      "title": "Status",
                      "short": true,
                      "value": "In Progress"
                    }
                  ]
                }
              ]
            }

      - name: Notify success
        if: success()
        uses: slackapi/slack-github-action@v1
        with:
          channel-id: ${{env.SLACK_CHANNEL_ID}}
          update-ts: ${{ steps.slack.outputs.ts }}
          payload: |
            {
              ${{env.PAYLOAD_BLOCKS}},
              "attachments": [
                {
                  ${{ env.ATTACHMENTS_AUTHOR }},
                  "color": "28a745",
                  "fields": [
                    {
                      "title": "Status",
                      "short": true,
                      "value": "Completed"
                    }
                  ]
                }
              ]
            }
      - name: Notify failure
        if: failure()
        uses: slackapi/slack-github-action@v1
        with:
          channel-id: ${{env.SLACK_CHANNEL_ID}}
          update-ts: ${{ steps.slack.outputs.ts }}
          payload: |
            {
              ${{env.PAYLOAD_BLOCKS}},
              "attachments": [
                {
                  ${{ env.ATTACHMENTS_AUTHOR }},
                  "color": "ff4032",
                  "fields": [
                    {
                      "title": "Status",
                      "short": true,
                      "value": "Failed"
                    }
                  ]
                }
              ]
            }
      - name: Notify cancelled
        if: cancelled()
        uses: slackapi/slack-github-action@v1
        with:
          channel-id: ${{env.SLACK_CHANNEL_ID}}
          update-ts: ${{ steps.slack.outputs.ts }}
          payload: |
            {
              ${{env.PAYLOAD_BLOCKS}},
              "attachments": [
                {
                  ${{ env.ATTACHMENTS_AUTHOR }},
                  "color": "89949f",
                  "fields": [
                    {
                      "title": "Status",
                      "short": true,
                      "value": "Cancelled"
                    }
                  ]
                }
              ]
            }
```
