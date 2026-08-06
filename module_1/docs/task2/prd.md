# Product Requirements Document

## Workflow Description

This workflow inspects the project's package.json file, identifies the available npm scripts, and summarizes their purpose without modifying any project files.

## Trigger

The workflow starts when a developer asks the agent to review package.json.

## Decision Events

1. If package.json exists, the agent reads the file and identifies all scripts.
2. If package.json is missing, the agent reports the error.
3. If scripts are found, the agent explains their purpose.
4. The agent does not modify any project files.

## Ordered Actions

1. Open package.json.
2. Locate the scripts section.
3. List each available script.
4. Explain the purpose of each script.
5. Produce a short summary.
6. Confirm that no files were modified.

## Acceptance Criteria

- The agent reads package.json successfully.
- Every npm script is listed.
- Each script has a short explanation.
- The summary is clear and accurate.
- No project files are modified.