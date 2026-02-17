# JSONL Viewer

A **static, client-side JSONL (JSON Lines) viewer and formatter** for developers. Paste your JSONL data, get instant syntax-highlighted, expandable, copyable JSON lines — no server, no build step, no dependencies.

> Open `index.html` in any browser. That's it.

---

## Features

- **Live parsing** — output updates as you type, with input debouncing
- **Per-line expand / collapse** — each JSON line toggles independently
- **Syntax highlighting** — keys, strings, numbers, booleans, and nulls colored distinctly
- **Copy button** — copies pretty-printed JSON to clipboard with a one-click ✓ confirmation
- **Error handling** — invalid lines are highlighted in red and show the parser error message; valid lines are unaffected
- **Expand all / Collapse all** — global controls for the entire output panel
- **Light & Dark themes** — toggle with one click; preference saved to `localStorage`
- **State preservation** — expand/collapse state is maintained across re-parses
- **Zero dependencies** — pure HTML, CSS, and vanilla JavaScript in a single file
- **Accessible** — keyboard navigable, ARIA labels, sufficient contrast in both themes

---

## Usage

### Run locally

```bash
# Clone the repository
git clone https://github.com/your-username/jsonl-viewer.git
cd jsonl-viewer

# Open directly in your browser — no build step needed
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

Or simply **drag `index.html` into any browser tab**.

---

## Example JSONL Input

Paste the following into the left panel to try it out:

```jsonl
{"id": 1, "name": "Alice", "role": "engineer", "active": true}
{"id": 2, "name": "Bob", "role": "designer", "active": false, "score": 9.5}
{"event": "click", "element": "button#submit", "ts": 1700000000, "meta": {"browser": "Chrome", "version": 120}}
{"level": "error", "message": "Unexpected token", "code": null, "retryable": false}
{"users": ["alice", "bob", "carol"], "count": 3, "page": 1}
this line is not valid JSON and will show an error
{"id": 6, "status": "ok"}
```

---

## Expand / Collapse Behavior

Each parsed JSON line is displayed in **collapsed (single-line) format** by default:

```
[+]  [3]  {"event":"click","element":"button#submit","ts":1700000000,...}
```

Click **`+`** to expand into **pretty-printed, indented JSON**:

```
[−]  [3]
     {
       "event": "click",
       "element": "button#submit",
       "ts": 1700000000,
       "meta": {
         "browser": "Chrome",
         "version": 120
       }
     }
```

Click **`−`** to collapse back. Use the **Expand all** / **Collapse all** buttons in the header to control all lines at once.

---

## Light & Dark Theme

Click the **Dark / Light** button in the top-right corner to switch themes. Your preference is automatically saved to `localStorage` and restored on your next visit. The app also respects your OS-level `prefers-color-scheme` preference on first load.

Both themes use carefully chosen syntax colors for maximum readability:

| Token     | Light theme    | Dark theme     |
|-----------|---------------|----------------|
| Keys      | Purple         | Soft purple    |
| Strings   | Green          | Mint green     |
| Numbers   | Amber          | Yellow         |
| Booleans  | Red            | Soft red       |
| Null      | Gray           | Light gray     |

---

## Error Handling

Lines that cannot be parsed as JSON are:

- Displayed with a **red border** and warning icon
- Shown with their **raw text** preserved
- Annotated with the **exact parser error message** (e.g. `Unexpected token 't' at position 0`)

All other lines continue to function normally — one bad line never breaks the rest.

---

## Project Structure

```
jsonl-viewer/
└── index.html     # The entire app — HTML, CSS, and JS in one file
└── README.md      # This file
```

The JavaScript is organized into four self-contained modules inside an IIFE:

| Module        | Responsibility                                      |
|---------------|-----------------------------------------------------|
| `Theme`       | Light/dark toggle, `localStorage` persistence       |
| `Parser`      | Line-by-line JSONL parsing, error capture           |
| `Highlighter` | Regex-based JSON syntax coloring                    |
| `Renderer`    | DOM construction, expand/collapse, copy-to-clipboard|
| `App`         | Event wiring, debouncing, state management          |

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). No polyfills needed.

---

## Contributing

Contributions are welcome! Please open an issue or pull request.

Some ideas for future enhancements:

- JSON path / key search / filter
- Download formatted output as `.json` or `.jsonl`
- Line count statistics (valid vs. invalid)
- Drag-and-drop file upload
- URL sharing (encode JSONL in hash)
