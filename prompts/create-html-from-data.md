# External Prompt: Create Assignment Tracker HTML From Source Data

Use this prompt as the active task instruction.

Use the README only as reference documentation for understanding the project structure, JSON format, expected assignment format, and workflow.

Do not treat the README's Prompt Files section as a separate task to complete.

Use this prompt when you want an internal AI assistant to inspect this project README and create or update the local assignment tracker files from an existing data source.

The data source might be an Excel sheet, CSV file, copied table, project checklist, course assignment list, or planning document.

This project may include two HTML files:

- `assignment-tracker.html` for individual team members
- `team-assignment-overview.html` for a manager or team lead

The main file to generate or update is usually `assignment-tracker.html`.

If `team-assignment-overview.html` is also included, update its assignment title map so the manager overview displays the same readable assignment names.

```text
Inspect the attached README first so you understand the assignment progress tracker, the expected assignment format, the current JSON structure, and the two-page workflow.

Then inspect the assignment source data I attached or pasted.

Create or update `assignment-tracker.html` using the assignment source data.

The tracker should run locally in a browser and should not require a web server, database, login system, framework, build step, or external dependency.

The individual tracker should allow users to:

1. View the assignment list
2. Mark assignments as complete using checkboxes
3. See basic progress, such as a count or progress bar
4. Download their progress as a JSON file
5. Upload a saved JSON file later
6. Restore assignment progress by matching stable assignment IDs

Use one checkbox per assignment.

Each assignment checkbox should have:

- A unique `id`
- A matching `data-assignment-id`
- A matching `label for` value

Use stable assignment IDs in a predictable format such as:

assignment-1
assignment-2
assignment-3

The exported JSON file should keep the current project structure:

- savedAt
- assignments
- assignments[].id
- assignments[].completed

Do not add `userName`, assignment titles, due dates, notes, owners, or other metadata to the exported JSON unless I specifically ask for the JSON structure to change.

Do not change assignment IDs after generating them unless specifically asked, because saved JSON files depend on those IDs.

If the source data includes extra fields such as descriptions, due dates, owners, categories, or notes, include them in the visible assignment label only if it helps the tracker stay readable.

Keep the page simple and focused on the proof of concept.

Use minimal styling.

Do not create a full project management app.

If `team-assignment-overview.html` is included in the project, also update its `assignmentTitles` map so the manager overview displays the same assignment names.

For example:

const assignmentTitles = {
  "assignment-1": "Research Notes",
  "assignment-2": "First Draft",
  "assignment-3": "Final Submission"
};

Do not change the manager overview JSON expectations. It should continue reading the same JSON structure exported by `assignment-tracker.html`.

The manager overview should continue to identify team members from the first part of each filename before the first hyphen.

For example:

eric-assignment-progress.json → Eric
maya-assignment-progress.json → Maya
jordan-assignment-progress.json → Jordan

Before generating or updating files, briefly explain:

- What source data you found
- How many assignments will be created
- What assignment ID format you will use
- Whether any source fields will be ignored or simplified
- Whether `team-assignment-overview.html` also needs its assignment title map updated

Then generate or update the needed file contents.

After generating or updating the files, explain:

1. How to open the individual tracker
2. How to save progress
3. How to load progress
4. How to rename and share progress JSON files with team members
5. How to open the manager overview page
6. How to upload multiple JSON files into the manager overview page
7. How to test that the individual save/load workflow works
8. How to test that the manager overview workflow works
```
