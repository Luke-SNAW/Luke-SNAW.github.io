
```yml
name: Release Info
env:
  SLACK_CHANNEL_ID: ${{ SLACK_CHANNEL_ID }}
  SLACK_BOT_TOKEN: ${{ secrets.SLACK_NOTIFICATIONS_BOT_TOKEN }}
  # https://api.slack.com/reference/messaging/payload
  # https://docs.github.com/ko/rest/actions/workflow-runs?apiVersion=2022-11-28
on:
  release:
    types: [created, edited]

jobs:
  publish:
    runs-on: ubuntu-latest
    timeout-minutes: 2
    steps:
      - name: Notify release
        uses: slackapi/slack-github-action@v1
        with:
          channel-id: ${{env.SLACK_CHANNEL_ID}}
          payload: |
            {
              "blocks": [
                {
                  "type": "header",
                  "text": {
                    "type": "plain_text",
                    "text": "📖 Release [Project] ${{ github.event.release.name }}"
                  }
                },
                {
                  "type": "section",
                  "text": {
                    "type": "mrkdwn",
                    "text": ${{ toJSON(github.event.release.body) }}
                  }
                },
                {
                  "type": "actions",
                  "elements": [
                    {
                      "type": "button",
                      "text": {
                        "type": "plain_text",
                        "text": "📖 Release link"
                      },
                      "url": "${{ github.event.release.html_url }}"
                    }
                  ]
                }
              ]
            }
```
