<!--
SPDX-FileCopyrightText: 2026 German Federal Office for Information Security (BSI) <https://www.bsi.bund.de>
Software-Engineering: 2026 Intevation GmbH <https://intevation.de>

SPDX-License-Identifier: Apache-2.0
-->

# GitHub Action for AI Contribution Detection

A GitHub Action that detects whether commits in a pull request were (co-)authored by an LLM.

## How it works

The action inspects every commit between the PR base and checks:

- Co-authorship: `Co-authored-by:` lines are matched against a list of known patterns
- Authorship: Compares commit authors with a list of known LLM names

If a match is found, the suspicious commit and the matching pattern are reported.

## Usage

Add it to a workflow triggered on `pull_request`:

```yaml
name: Check for AI co-authorships

on:
  pull_request:

permissions: {}

jobs:
  ai-coauthorship-check:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - uses: Intevation/ai-contribution-action@main
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `fail-on-detection` | No | `true` | Exit with a non-zero status code when LLM co-authorship is detected. Set to `false` to only report. |
| `comment-on-detection` | No | `false` | Post a PR comment when LLM (co-)authorship is detected. |

### Post a PR comment on detection

Requires `pull-requests: write` permission:

```yaml
jobs:
  ai-coauthorship-check:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - uses: Intevation/ai-contribution-action@main
        with:
          comment-on-detection: true
```


## License

```
SPDX-License-Identifier: Apache-2.0

SPDX-FileCopyrightText: 2025 German Federal Office for Information Security (BSI) <https://www.bsi.bund.de>
Software-Engineering: 2025 Intevation GmbH <https://intevation.de>
```
