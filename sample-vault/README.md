# Bases Sidebar View Plugin - Testing Instructions

## Setup

1. The sample vault is configured with:
   - 5 test notes in the `Projects/` folder
   - A base file: `Everything tagged project.base`
   - The Bases Sidebar View plugin installed

## How to Test

### Step 1: Open Obsidian
Open the `sample-vault` folder as a vault in Obsidian

### Step 2: Enable the Plugin
1. Go to Settings → Community Plugins
2. Enable "Bases Sidebar View"

### Step 3: Open the Base File
1. Open `Everything tagged project.base`
2. You should see the default view

### Step 4: Switch to Sidebar View
1. Click on the view type dropdown (currently shows "Table")
2. Select "Sidebar" from the list
3. The view should change to show:
   - **Left panel**: List of all notes tagged with `#project`
   - **Right panel**: Preview of the selected note

### Step 5: Interact with Notes
- Click any note in the left panel to preview it
- Click "Add" to create a new note with the `#project` tag
- Click the preview content to open the note in the main editor

## Troubleshooting

### No notes showing in the left panel?

1. Open the Developer Console: `Cmd+Option+I` (Mac) or `Ctrl+Shift+I` (Windows/Linux)
2. Look for console messages:
   - `onDataUpdated called`
   - `Number of groups: X`
   - `Total entries rendered: X`

3. Check the base file filter:
   - Open `Everything tagged project.base`
   - It should contain: `filter: tag(project)`
   - NOT: `filter: tag(#project)` (no # symbol)

4. Check the notes have the correct tags:
   - Open any note in `Projects/` folder
   - Frontmatter should have:
     ```yaml
     ---
     tags:
       - project
     ---
     ```

### Notes still not showing?

The filter syntax might need adjustment. Try:
- `filter: tag(project)` - current
- `filter: "#project"` - alternative
- Check Obsidian's Bases documentation for correct filter syntax

## File Structure

```
sample-vault/
├── .obsidian/
│   ├── plugins/
│   │   └── bases-sidebar-view/
│   │       ├── main.js
│   │       └── manifest.json
│   └── community-plugins.json
├── Projects/
│   ├── Untitled.md (tagged #project)
│   ├── eqwqfeq.md (tagged #project)
│   ├── qfwqfe.md (tagged #project)
│   ├── Explore page Revamp.md (tagged #project)
│   └── explore page.md (tagged #project)
└── Everything tagged project.base
```

## Expected Behavior

- **Left Panel**:
  - Header with title and "Add" button
  - List of notes grouped (if grouping is configured)
  - Each note shows: title, date, and metadata
  - Selected note is highlighted with accent color

- **Right Panel**:
  - Editable title field
  - Rendered markdown content
  - Click to open in main editor

## Known Limitations

- Right panel shows read-only preview (click to edit in main workspace)
- Obsidian's API limitations prevent full embedded editing
