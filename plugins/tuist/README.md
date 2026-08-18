# Tuist

Work with [Tuist](https://tuist.dev) projects from Cursor.

## Skills

| Skill | What it does |
| --- | --- |
| `migrate` | Migrates an existing Xcode project to a Tuist generated workspace, mapping external dependencies and validating that it still builds and runs |
| `generated-projects` | Day-to-day guidance for generated workspaces: `tuist generate`, `xcodebuild` invocations, buildable folders, target tags |
| `debug-generated-project` | Reproduces a generation or post-generation build failure locally and triages it as a bug, a misconfiguration, or something for the Tuist team |
| `compare-builds` | Diffs two Xcode builds for duration regressions, cache changes, and new issues |
| `compare-gradle-builds` | Diffs two Gradle builds for duration regressions, cache changes, and task outcome differences |
| `compare-generations` | Diffs two `tuist generate` runs and root-causes cache invalidation |
| `compare-cache-runs` | Diffs two `tuist cache` runs and root-causes cache invalidation |
| `compare-test-runs` | Diffs two test runs for new failures, newly flaky tests, fixed tests, and duration regressions |
| `compare-test-case` | Diffs a single test case across two branches: status, duration, flakiness, failure details |
| `compare-bundles` | Diffs two app bundles for size changes and new or removed artifacts |
| `analyze-selective-testing` | Explains which test targets selective testing skipped or ran, and why selection regressed |
| `fix-flaky-tests` | Finds flaky tests from Tuist test insights, works out the root cause, and applies targeted fixes |

Cursor picks a skill from what you ask for, so "compare the builds on main and my branch" is enough to get started. The comparison skills resolve run IDs, dashboard URLs, and branch names alike, and fall back to the default branch when you only name one side.

## MCP

`mcp.json` registers the hosted Tuist MCP server at `https://tuist.dev/mcp`, and Cursor prompts you to sign in with your Tuist account the first time it is used.

The skills reach for the `tuist` CLI first, since that keeps them usable on any machine that has Tuist installed. The MCP server fills the gaps: `compare-gradle-builds` runs entirely through it, `compare-generations` and `compare-cache-runs` use it for per-target module cache detail that the CLI does not expose, and it also serves Tuist documentation and source search for questions the skills do not cover.

## Requirements

- The [Tuist CLI](https://tuist.dev/en/docs/guides/install-tuist), for both local generation and the dashboard queries the skills run.
- A [Tuist account](https://tuist.dev) connected to your project, authenticated with `tuist auth login`, for anything that reads builds, test runs, bundles, or cache runs.
