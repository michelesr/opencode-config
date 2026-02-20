---
name: atlassian-cli
description: Use Atlassian Command Line Interface (ACLI, `acli`) for Atlassian Cloud.
---

# Atlassian CLI (acli)

Use `acli` to automate and operate Atlassian Cloud workflows from the terminal (Jira, Admin, and Rovo Dev).

## Workflow

1. Discover the exact command/flags via `acli help ...` and `--help`.
2. Prefer machine-readable output (`--json`) for automation; parse with `jq`.
3. Handle bulk operations with `--ignore-errors` where appropriate; capture trace IDs on unexpected errors.

## Some useful commands

- Retrieve ticket data `acli jira workitem view <ticket>`
- If you need specific fields for a ticket, use `--json --fields <fields>`, e.g `--json --fields duedate,customfield_1234`
- If you need linked work items for a ticket, use `acli jira workitem link list --json --key <ticket>`
- If you need child work items for an epic, use `acli jira workitem search --json --jql "'Epic Link' = <ticket>"`

## Command Discovery Pattern

- Show top-level help: `acli --help`
- Show product help: `acli jira --help`, `acli admin --help`, `acli rovodev --help`
- Show deep help: `acli jira workitem create --help`
- Use `acli help [path]` when unsure where a command lives.

## Automation Patterns

- Chain commands with `&&` when later steps must only run on success.
- Redirect tabular output (`--csv`) to files.
- Use `--json | jq ...` to extract specific fields.

Read `references/automation.md`.

## Troubleshooting

- Capture trace IDs from unexpected errors for support tickets.
- Use `--ignore-errors` for bulk operations where partial success is acceptable.
- Use `--generate-input-json` / `--generate-json` on commands that support JSON-driven workflows.
