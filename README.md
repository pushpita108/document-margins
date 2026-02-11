# Document Margins

A browser bookmarklet that adds AI-powered margin notes to any web page. Highlight text to create notes, ask follow-up questions powered by Google Gemini, and generate executive summaries of documents combined with your annotations.

## Features

- **Margin Notes** — Select text on any page to create a note anchored to that position
- **AI Chat** — Ask follow-up questions about highlighted text; responses are powered by Google Gemini
- **AI Synthesis** — Generate a comprehensive executive summary combining the full document with all your notes, downloaded as a `.txt` file
- **Persistence** — Notes are saved to `localStorage` and restored on subsequent visits

## Setup

1. Get a Google Gemini API key from https://aistudio.google.com/apikey
2. On first run, the bookmarklet will prompt you to enter your API key — it's stored in your browser's `localStorage` and never leaves your machine

## Usage

### Option A: Direct Bookmarklet

1. Create a new bookmark in your browser
2. Paste the contents of `bookmarklet.js` as the URL
3. Navigate to any page, highlight text, and click the bookmarklet

### Option B: Loader Bookmarklet

1. Create a new bookmark with the contents of `loader-bookmarklet.js` as the URL
2. This loads the latest version from CDN each time

### Option C: Browser Console

Paste the contents of `script.js` directly into the browser's developer console.

## How It Works

Once activated on a page:

1. A **control panel** appears in the top-right corner with "AI Synthesis" and "Clear All" buttons
2. **Highlight any text** — a margin note card appears next to the selection
3. **Ask questions** — type in the note's text area and click "Ask" to chat with Gemini about the highlighted text
4. **AI Synthesis** — click the button to generate a summary of the entire document and all your notes

## Files

| File | Description |
|------|-------------|
| `script.js` | Readable source code (edit this) |
| `bookmarklet.js` | Minified version for production use |
| `loader-bookmarklet.js` | Lightweight loader that fetches `bookmarklet.js` from CDN |

## License

[MIT](LICENSE)
