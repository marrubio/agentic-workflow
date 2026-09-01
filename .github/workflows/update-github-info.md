---
name: update-github-info
description: Daily workflow to fetch latest GitHub blog updates and update site content
engine: copilot
tools:
  web-fetch: null
  edit: null
  github: null
safe-outputs:
  create-pull-request: null
network:
  allowed:
    - github.blog
    - github.com
on:
  schedule:
    - cron: daily
  workflow_dispatch:
---

## Overview

This workflow automatically fetches the latest GitHub blog posts and updates the site's GitHub info content. It creates a pull request for Mona to review all changes.

## Workflow Instructions

You are a GitHub content curator. Your task is to:

1. **Read the current notes** for context:
   - Read the file `notes/mona-notes.md` to understand the current project state and any special requirements

2. **Fetch latest GitHub updates** from these sources:
   - Web fetch: `https://github.blog/latest/`
   - Web fetch: `https://github.blog/changelog/`

3. **Update the site content**:
   - Edit the file `site/content/github-info.md` to include:
     - Summary of the latest GitHub blog posts
     - Key changelog items
     - Notable announcements or features
   - Keep the content concise and well-formatted in markdown
   - Maintain consistency with existing content style

4. **Create a pull request**:
   - Use the `create-pull-request` tool with `safe-outputs: true`
   - Title: "Update GitHub info from latest blog posts"
   - Body: Include a summary of what was updated
   - Assign the PR to Mona for review
   - Add labels: `documentation`, `automation`
   - Request Mona as a reviewer

5. **Validation**:
   - Ensure all markdown is properly formatted
   - Verify links are valid
   - Check that the content is up-to-date with the fetched data

## Notes

- Use web-fetch for reading external public guidance from github.blog
- Use the GitHub API tools for reading repository files instead of shell commands
- All changes are proposed through a pull request (safe-outputs mode) and do not write directly to main
- The workflow respects network configuration and only connects to github.blog and github.com
