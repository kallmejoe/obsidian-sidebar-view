# Debugging Guide - Why Notes Aren't Showing

## Current Status

✅ **What's Working:**
- Plugin is installed at: `sample-vault/.obsidian/plugins/bases-sidebar-view/`
- Plugin is enabled in community-plugins.json
- Bases core plugin is enabled
- 5 test notes exist in `Projects/` folder with `#project` tag
- Base file exists: `Everything tagged project.base`

❓ **What Needs Investigation:**
- Why notes aren't appearing in the sidebar view

## Step-by-Step Debugging

### 1. Check if Plugin is Loaded

**In Obsidian:**
1. Open Settings → Community Plugins
2. Verify "Bases Sidebar View" is in the list and enabled
3. If not, click "Reload app without saving" from Command Palette

### 2. Check if Sidebar View is Registered

**In Developer Console** (`Cmd+Option+I` or `Ctrl+Shift+I`):
1. Type: `app.viewRegistry`
2. Look for your custom view type in the registry
3. If the plugin loaded correctly, you should see console logs

### 3. Check Base File Filter

The base file filter syntax must match Obsidian's Bases query language:

**Current filter:** `tag(project)`

**Alternative filters to try:**
```
tag(#project)
```
or
```
file.tags.includes("project")
```
or
```
file.tags.contains("project")
```

**To test:**
1. Open `Everything tagged project.base`
2. Try each filter syntax above
3. Save and see if notes appear

### 4. Check Console Logs

When you open the Sidebar view, you should see in the console:
```
onDataUpdated called, groupedData: [...]
Number of groups: X
Entry: Projects/Untitled.md
Entry: Projects/eqwqfeq.md
... (etc)
Total entries rendered: 5
```

**If you see `Total entries rendered: 0`:**
- The filter is not matching any notes
- Try different filter syntaxes (see step 3)

**If you don't see any console logs:**
- The plugin didn't load
- The view wasn't switched to "Sidebar"
- Try reloading Obsidian

### 5. Verify View Selection

**In the Base file:**
1. Open `Everything tagged project.base`
2. Look at the toolbar - there should be a view selector dropdown
3. Click it and select "Sidebar" from the list
4. If "Sidebar" isn't in the list, the plugin registration failed

### 6. Check for JavaScript Errors

**In Developer Console:**
1. Look for red error messages
2. Common errors:
   - `TypeError: Cannot read property 'X' of undefined`
   - `Failed to load plugin`
   - Module errors

## Quick Test

**Create a simple test base:**

1. Create a new file: `Test.base`
2. Add this content (try different variations):

```
filter: tag(project)
```

Or try:
```
filter: file.tags.includes("project")
```

Or even simpler:
```
filter: ""
```
(This should show ALL files in your vault)

3. Open the file and switch view to "Sidebar"
4. Check console for logs

## Expected Console Output

```
onDataUpdated called, groupedData: [Array]
Number of groups: 1
Group entries: 5
Entry: Projects/Untitled.md
Entry: Projects/eqwqfeq.md
Entry: Projects/qfwqfe.md  
Entry: Projects/Explore page Revamp.md
Entry: Projects/explore page.md
Total entries rendered: 5
```

## Common Issues & Solutions

### Issue: "Sidebar" doesn't appear in view dropdown

**Solution:**
- Plugin didn't register correctly
- Check manifest.json is valid
- Reload Obsidian
- Check console for errors during plugin load

### Issue: View shows but left panel is empty

**Solution:**
- Filter syntax is wrong
- Try filter: `""` to show all files
- Check console logs for the actual data being received

### Issue: Console shows "Total entries rendered: 0"

**Solution:**
- No files match the filter
- Try a simpler filter or `filter: ""`
- Verify notes actually have the `project` tag

### Issue: Clicking notes does nothing

**Solution:**
- Check console for "Note clicked: ..." message
- If you see the message but nothing happens, there's an error in `openFileInEditor`
- Check for JavaScript errors in console

## Next Steps

1. Open Developer Console
2. Open `Everything tagged project.base`  
3. Switch to "Sidebar" view
4. Share the console output

This will tell us exactly what's happening!
