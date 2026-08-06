\# Product Requirements Document



\## Workflow Description



This workflow runs the React project's production build command, reports whether the build succeeds, summarizes any warnings or errors, and recommends whether the project is ready for the next step.



\## Trigger



The workflow starts when a developer manually asks Claude Code to review the project build from the repository root inside the sandboxed container.



\## Decision Events



1\. If the build succeeds, the agent reports the successful result, summarizes any warnings, and recommends whether the project is ready to proceed.



2\. If the build fails, the agent reports the errors, explains the likely blocking issues, and recommends against proceeding.



3\. If the build cannot run because of an environment or dependency problem, the agent reports the issue and does not claim that the build passed or failed.



4\. If warnings are present, the agent separates them from build errors.



\## Ordered Actions



1\. Confirm that the repository files are accessible inside the sandboxed container.



2\. Identify the production build command from `package.json`.



3\. Run `npm run build` from the repository root.



4\. Capture the build output and final result.



5\. Determine whether the build succeeded, failed, or could not complete.



6\. Summarize all warnings and errors shown in the build output.



7\. Record the generated build file sizes when available.



8\. Produce a final recommendation about whether the project is ready for the next step.



9\. Confirm that no source files or configuration files were modified.



\## Acceptance Criteria



\* The agent runs `npm run build` from the repository root.



\* The reported build result matches the actual command output.



\* All warnings and errors shown in the build output are included in the summary.



\* Warnings are clearly separated from blocking errors.



\* The recommendation is consistent with the build result.



\* The agent does not modify source code or configuration files.



\* The output is clear enough for another developer to understand the build status without reading the complete terminal output.



