# Notify PR Review (Customized)

This project is based on [naver/notify-pr-review](https://github.com/naver/notify-pr-review),
licensed under the Apache License 2.0.

## Usage

1. 메시지 전달을 위해 `SLACK_BOT_TOKEN` 이름의 secret을 세팅하세요.

> 세팅할 Repo > Settings > Secrets > New repository secret

이때, Value는 슬랙에서 제공하는 `xoxb-` 형태의 토큰이어야 합니다.

2. `.github/workflow/notify-pr-review.yml` 파일을 만드세요:

```yml
name: notify pr review

on:
  pull_request:
    types: [review_requested]

jobs:
  notify:
    runs-on: [ubuntu-latest]
    steps:
      - name: Notify PR Review
        uses: pierrot-company/notify-pr-review@v1.2.1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          slackBotToken: ${{ secrets.SLACK_BOT_TOKEN }}
          nameMapping: '{"pierrot":"joker"}'
```

## Input

### `token`

GitHub Token to access the repository

### `slackBotToken`

Slack Bot Token for sending messages

e.g. `xoxb-...`

### `nameMapping`

A JSON string mapping GitHub usernames to Slack usernames

```json
{
  "githubName": "slackName"
}
```

e.g. `{"pierrot": "joker"}`

## Modifications

The following features were added or modified:

- Support Slack Name Mapping

## License

This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
