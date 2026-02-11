# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A browser bookmarklet that adds AI-powered margin notes to any web page. Users highlight text to create notes, ask follow-up questions via Google Gemini API, and generate executive summaries of documents with their annotations.

## Development

There is no build system, package manager, test framework, or linter. The project is three standalone JavaScript files meant to run directly in the browser.

### Workflow

- Edit `script.js` (the readable source)
- Minify it into `bookmarklet.js` for production use
- `loader-bookmarklet.js` loads `bookmarklet.js` from jsdelivr CDN (`plawanrath/document-margins@main`)

To test changes: paste the contents of `script.js` into the browser console or create a bookmarklet from it.

## Architecture

Everything runs inside a single self-executing IIFE in `script.js` (179 lines):

1. **Storage & Styles** (lines 5-35) — Loads/saves notes from `localStorage` (key: `_marginalia_notes`), injects CSS
2. **Markdown converter** (lines 37-54) — `md2html()` converts AI responses to HTML via regex chain
3. **Chat rendering** (lines 56-62) — `renderHistory()` renders user/AI message history in note cards
4. **AI Synthesis** (lines 64-108) — `generateAISummary()` scrapes page text (up to 15k chars), combines with all notes, calls Gemini API, downloads result as `.txt` file
5. **Note injection** (lines 110-156) — `injectNote()` creates margin note UI with close button, chat area, and follow-up question input; each question sends highlight + page context (4k chars) to Gemini
6. **Init** (lines 158-179) — Creates control panel (AI Synthesis / Clear All buttons), restores saved notes, captures current text selection as new note

### Key Details

- API: Google Generative AI v1beta, model `gemini-flash-latest`
- API key is prompted on first use and stored in `localStorage` (key: `_marginalia_api_key`)
- Notes are positioned absolutely using `window.scrollY + selection rect top`
- UI is injected directly into the host page's DOM with high z-index values
