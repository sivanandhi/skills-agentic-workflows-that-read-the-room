---
name: update-github-info
description: Refresh the GitHub Info page from GitHub Blog, Changelog, and Awesome Copilot updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine: copilot
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
    allowed:
      - get_file_contents
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
---

# Update GitHub Info

Maintain the site's GitHub information page with concise, practical updates for developers.

## Research

1. Read `notes/mona-notes.md` using the GitHub repository API tool `get_file_contents`. Follow its editorial guidance.
2. Read the current `site/content/github-info.md` using `get_file_contents` so you preserve its structure and avoid duplicating existing content.
3. Use `web-fetch` to fetch https://github.blog/latest/.
4. Use `web-fetch` to fetch https://github.blog/changelog/.
5. Use `web-fetch` to fetch https://awesome-copilot.github.com/workflows/.
6. Use the GitHub repository API tools for any repository guidance or reference files you need. Do not use terminal commands, the GitHub CLI, or sandboxed shell commands for GitHub API reads.

## Update

Use the edit tool to update `site/content/github-info.md` with only useful, current items from the fetched GitHub Blog, Changelog, and Awesome Copilot workflows pages. Keep summaries short and practical, explain how each item helps developers learn GitHub faster, and mention the source for every item. Preserve the existing Markdown structure and remove or refresh stale entries rather than growing the page indefinitely.

Do not modify workflow files or unrelated files. Review the resulting diff for accidental changes before requesting the pull request.

## Review

Use the `create-pull-request` safe output to open one pull request containing the change for Mona to review. Use a clear title such as `Update GitHub info from GitHub Blog and Changelog`, and describe the sources reviewed and the key updates in the pull request body. Never write directly to the default branch.
