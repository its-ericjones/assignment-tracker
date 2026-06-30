# External Prompt: Reuse Assignment Tracker Logic

Use this prompt as the active task instruction.

Use the README only as reference documentation for understanding the project structure, JSON format, expected assignment format, and workflow.

Do not treat the README's Prompt Files section as a separate task to complete.

Use this prompt when you want an internal AI assistant to inspect this project README and apply the same local HTML/JSON tracking logic to another existing tracker.

This project may include two related workflows:

- Individual progress tracking from `assignment-tracker.html`
- Manager/team overview from `team-assignment-overview.html`

Use the individual tracker logic when the existing project needs checkbox progress, JSON export, and JSON import.

Use the manager overview logic when the existing project needs to upload multiple team member JSON files and display team progress at a glance.

Do not merge both workflows into the existing tracker unless I specifically ask for both.

```text
Inspect the attached README first so you understand the assignment progress tracker, the manager overview page, the current JSON structure, and the local browser-only workflow.

Then inspect the existing tracker files I attached.

Use the README as a reference, but do not copy the entire proof-of-concept project unless needed.

Preserve the existing tracker’s structure, layout, styling, and workflow as much as possible.

Do not add a server, database, login system, framework, build step, or external dependency.

First identify which workflow I am asking for:

1. Individual progress save/load
2. Manager/team overview
3. Both workflows

If I did not clearly ask for both workflows, only implement the workflow that matches my request.

For individual progress save/load, reuse the logic from `assignment-tracker.html`.

The final individual tracker behavior should allow users to:

1. Mark assignments as complete
2. Download their progress as a JSON file
3. Upload a saved JSON file later
4. Restore assignment progress by matching stable assignment IDs

The exported JSON file should keep the current project structure:

- savedAt
- assignments
- assignments[].id
- assignments[].completed

Do not add `userName`, assignment titles, due dates, notes, owners, or other metadata to the exported JSON unless I specifically ask for the JSON structure to change.

When loading a JSON file:

- Match saved assignment IDs to the current tracker’s assignment IDs.
- Restore the completed state for matching assignments.
- Ignore unknown assignment IDs instead of breaking the page.
- Leave assignments unchanged if they are not included in the uploaded JSON file.

For manager/team overview, reuse the logic from `team-assignment-overview.html`.

The final manager overview behavior should allow a user to:

1. Upload multiple progress JSON files at once
2. Derive each team member name from the filename
3. Display each team member as a column
4. Display each assignment as a row
5. Show whether each team member completed each assignment
6. Show a progress bar and percentage for each assignment across the team

The manager overview should continue to read the same JSON structure exported by the individual tracker.

It should identify each team member from the first part of the filename before the first hyphen.

For example:

eric-assignment-progress.json → Eric
maya-assignment-progress.json → Maya
jordan-assignment-progress.json → Jordan

If readable assignment names are needed in the manager overview, use an assignment title map inside the HTML or existing project code.

For example:

const assignmentTitles = {
  "assignment-1": "Research Notes",
  "assignment-2": "First Draft",
  "assignment-3": "Final Submission"
};

Do not require assignment titles to be added to the JSON unless I specifically ask for the JSON structure to change.

Before editing, explain:

- Which workflow you are implementing
- Where assignments are rendered
- How completion state is currently stored
- Whether assignments already have stable IDs
- Where the export/import controls should go, if implementing individual save/load
- Where the multiple-file upload control and team table should go, if implementing manager overview
- Whether the existing tracker already has any persistence behavior

Then make the smallest changes needed to support the requested workflow.

After making the change, explain:

1. What files changed
2. What logic was added
3. How the JSON export works, if individual save/load was added
4. How the JSON import works, if individual save/load was added
5. How the multiple-file team overview works, if manager overview was added
6. How team member names are derived from filenames, if manager overview was added
7. How to test the updated workflow
```
