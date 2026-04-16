# QuartoAnnotationWebsite

**Annotate Quarto Presentations** — a lightweight Flask web app for highlighting text and adding notes to Quarto HTML presentations directly in your browser.

## Features

- 📤 **Upload** any Quarto-rendered HTML presentation
- 🖊️ **Highlight** text in five colours (yellow, green, blue, pink, orange)
- 📝 **Add notes** to each highlight via a floating toolbar + modal
- 💾 **Persist** annotations in a local SQLite database
- 📋 **Sidebar** lists all annotations; click to flash the highlight in context
- ✏️ **Edit or delete** annotations at any time
- 🎯 **Sample presentation** included — open the app and start annotating immediately

## Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run the development server
python app.py

# 3. Open http://localhost:5000 in your browser
```

The app creates a SQLite database (`instance/annotations.db`) and an `uploads/` folder automatically on first run.

## Project Structure

```
QuartoAnnotationWebsite/
├── app.py                          # Flask application & REST API
├── requirements.txt
├── sample/
│   └── sample_presentation.html   # Built-in demo presentation
├── static/
│   ├── css/style.css               # All UI styles
│   └── js/annotator.js             # Client-side annotation engine
└── templates/
    ├── index.html                  # Home / upload page
    └── viewer.html                 # Presentation viewer + sidebar
```

## API Endpoints

| Method | URL | Description |
|--------|-----|-------------|
| `GET` | `/api/annotations/<id>` | List annotations for a presentation |
| `POST` | `/api/annotations` | Create a new annotation |
| `PUT` | `/api/annotations/<id>` | Update note/colour of an annotation |
| `DELETE` | `/api/annotations/<id>` | Delete an annotation |

## How It Works

1. Quarto HTML presentations are served inside an `<iframe>`.
2. The annotation engine listens for `mouseup` events inside the iframe.
3. When text is selected, a floating toolbar appears for colour selection.
4. Clicking **Annotate** opens a modal to optionally add a note.
5. The selection is anchored using **XPath** so highlights survive page reloads.
6. Annotations are stored in SQLite and re-applied on every page load.
