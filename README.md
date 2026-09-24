<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/bugmole-lockup-dark.svg">
    <img alt="Bugmole" src="assets/bugmole-lockup-light.svg" width="320">
  </picture>
</p>

<p align="center"><strong>Our moles find the bugs before your users do.</strong></p>

<p align="center">
  <a href="https://bugmole.com/docs/">Docs</a> ·
  <a href="https://bugmole.com">Website</a> ·
  <a href="https://discord.gg/q9k5ngWKQ">Discord</a> ·
  <a href="https://www.youtube.com/@bugmole">YouTube</a> ·
  <a href="https://bugmole.com/docs/changelog/">Changelog</a>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@bugmole/cli"><img alt="npm" src="https://img.shields.io/npm/v/@bugmole/cli?label=%40bugmole%2Fcli&color=152233"></a>
  <a href="https://discord.gg/q9k5ngWKQ"><img alt="Discord" src="https://img.shields.io/badge/chat-Discord-5865F2"></a>
</p>

Bugmole explores your web app the way a real user does, writes each journey down as a readable flow, and runs it across browsers and devices in parallel. When something breaks, you get the screenshots, video and logs to see why.

- **Explore:** point Bugmole at your app and it maps the journeys a user can take.
- **Plan:** each journey becomes a flow file you can read, review and edit. No CSS selectors.
- **Run:** Chromium, Firefox, WebKit, Edge and emulated phones, all at once, locally or in CI.
- **Debug:** every run keeps its own screenshots, video and log, plus a plain-language report.
- **Works with your AI assistant:** connect Claude, ChatGPT, Cursor or Codex over MCP.

## Get started

### Bugmole Cloud (recommended)

Sign up at **[app.bugmole.com](https://app.bugmole.com)**, create a project, then connect the machine that can reach your app:

```bash
npm install -g @bugmole/cli
bugmole init
bugmole serve
```

`bugmole init` pairs this machine with your project (it opens the browser for you). `bugmole serve` keeps a worker running that picks up the test runs you start from the dashboard. Your app and its artifacts stay on your machine.

Requires Node.js 22 or newer. The `bm` command is a shortcut for `bugmole`.

### From the command line

```bash
bugmole --mode explore     # map the journeys in your app
bugmole --mode plan        # turn one into an executable plan
bugmole --mode run --plan-id <plan> --browsers chromium,firefox,webkit
```

Bugmole installs Chromium. For the other engines, run once per machine:

```bash
npx playwright install firefox webkit msedge
```

Full walkthrough: **[Getting started](https://bugmole.com/docs/getting-started/)**.

### From your AI assistant

Add Bugmole as an MCP server and ask your assistant to test something:

```bash
claude mcp add --transport http bugmole https://api.bugmole.com/mcp
```

Setup for ChatGPT, Claude Desktop, Cursor and Codex: **[Use Bugmole from your AI assistant](https://bugmole.com/docs/ai-assistants/)**. Ready-made configs are in [`examples/mcp`](examples/mcp).

## What a flow looks like

```yaml
url: https://staging.example.com/projects
name: create-project
---
- launchApp
- tapOn: "New project"
- tapOn: "Project name"
- inputText: "My Project"
- tapOn: "Create"
- assertVisible: "Project created"
```

Steps find elements the way a person does, by a button's name, a field's label or visible text, so a restyled page doesn't break the test. Run a folder of flows against any environment:

```bash
bugmole --mode suite --flows spec/flows --base-url https://staging.example.com \
  --browsers chromium,firefox,webkit,msedge --devices "iPhone 15,Pixel 7"
```

More in [`examples/flows`](examples/flows) and **[Sample tests](https://bugmole.com/docs/sample-tests/)**.

## Run it in CI

Any CI that can run a shell step works. `bugmole --mode run` exits `1` unless the run is a clean pass.

```yaml
- run: npm install -g @bugmole/cli
- run: bugmole --mode run --plan-id "$BUGMOLE_PLAN_ID" --browsers chromium,firefox,webkit
  env:
    BUGMOLE_API_KEY: ${{ secrets.BUGMOLE_API_KEY }}
    BUGMOLE_PLAN_ID: ${{ vars.BUGMOLE_PLAN_ID }}
```

GitHub Actions, GitLab CI, Jenkins and CircleCI examples are in [`examples/ci`](examples/ci). For pull request checks without any pipeline changes, install the **[Bugmole GitHub App](https://bugmole.com/docs/github-app/)**.

## Docs

| | |
| --- | --- |
| [Getting started](https://bugmole.com/docs/getting-started/) | Install, pair a machine, first run |
| [CLI reference](https://bugmole.com/docs/cli/) | Every command and flag |
| [Configuration](https://bugmole.com/docs/configuration/) | Environments, secrets, config file |
| [Sample tests](https://bugmole.com/docs/sample-tests/) | Flow syntax, side by side with Playwright, Cypress and Selenium |
| [Discover and debug](https://bugmole.com/docs/discover-and-debug/) | Exploring an app and reading a failed run |
| [Continuous integration](https://bugmole.com/docs/continuous-integration/) | Running in any CI |
| [GitHub App](https://bugmole.com/docs/github-app/) · [GitLab](https://bugmole.com/docs/gitlab/) | Checks on pull and merge requests |
| [Slack](https://bugmole.com/docs/slack/) · [Microsoft Teams](https://bugmole.com/docs/microsoft-teams/) | Alerts |
| [Real devices](https://bugmole.com/docs/device-clouds/) | BrowserStack, Sauce Labs and other device clouds |
| [MCP](https://bugmole.com/docs/mcp/) | The local MCP server and its tools |
| [Plans and limits](https://bugmole.com/docs/plans-and-limits/) | Pricing and usage |

## Community

Bugmole is built in the open with the people who use it.

- **[Discord](https://discord.gg/q9k5ngWKQ)**: chat with the team and other users.
- **[Discussions](../../discussions)**: questions, ideas and show-and-tell.
- **[Issues](../../issues/new/choose)**: bug reports and feature requests. Inside the dashboard, **Report a bug** attaches screenshots, console logs and your environment for you.
- **Security:** please report vulnerabilities privately, see [SECURITY.md](SECURITY.md).
- **Email:** [hello@bugmole.com](mailto:hello@bugmole.com)
