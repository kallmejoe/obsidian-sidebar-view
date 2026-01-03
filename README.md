# Bases Sidebar View

A custom view for Obsidian Bases that displays your notes in a beautiful sidebar layout with live preview.

## Features

- **Split View Layout**: Browse notes in a sidebar while viewing content in a reading pane
- **Reading Mode by Default**: Notes open in clean, distraction-free reading mode
- **Resizable Sidebar**: Drag the divider to adjust the sidebar width to your preference
- **Smooth Navigation**: Switch between notes instantly without flickering
- **Hover Previews**: Hover over notes to see a quick preview
- **Properties Panel**: Toggle properties visibility from the Bases options
- **Persistent Settings**: Sidebar width and preferences are saved

## Installation

### Manual Installation

1. Download `main.js` and `manifest.json` from the latest release
2. Create a folder `bases-sidebar-view` in your vault's `.obsidian/plugins/` directory
3. Place the downloaded files in this folder
4. Reload Obsidian
5. Enable the plugin in Settings → Community Plugins

## Usage

1. **Create or open a Base** in your vault
2. Click the **view switcher** in the top-right corner of the Base
3. Select **"Sidebar"** view
4. Browse your notes in the left panel and read them in the right panel

### Adding the View to a Base

1. Open any Base file (e.g., `My Notes.base`)
2. Click the view options button (three dots or settings icon)
3. Choose "Sidebar" from the view types

### Options

Access view options from the Bases toolbar:

- **Group separator**: Customize the separator between metadata fields
- **Show properties**: Toggle the properties panel visibility

### Shortcuts

- **Click a note**: Open it in reading mode
- **Drag the divider**: Resize the sidebar
- **Click "Add"**: Create a new note in the current Base

## Development

Built with:
- TypeScript
- Obsidian API
- Bases API
- esbuild

### Building from Source

```bash
npm install
npm run build
```

### Development Mode

```bash
npm run dev
```

This will watch for changes and rebuild automatically.

## Credits

Created for the Obsidian Bases plugin to provide a better note browsing experience.

## License

MIT
