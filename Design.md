# Design.md

## 1. Product Vision

**NovelStudio** is a cross-platform desktop IDE for novelists and storytellers, built on .NET 8 and Avalonia. Authors organize stories by book, chapter, and scene, manage characters and world notes, and write in a rich, distraction-free environment. A built-in AI assistant (powered by OpenRouter LLM) helps with brainstorming, suggestions, and creative blocks—always opt-in and privacy-focused.

---

## 2. Core Goals & Success Criteria

| Goal                          | Success Metric                                                          |
|-------------------------------|-------------------------------------------------------------------------|
| Seamless project organisation | Create, rename, move, delete books/chapters/scenes instantly            |
| Rich text editing             | Formatting (bold, italic, headings, lists, quotes), smooth undo/redo    |
| Multidocument editing         | Open ≥ 5 files at once, switch tabs instantly                           |
| Inline spellcheck             | NHunspell/LanguageTool.NET with <100 ms latency for 10k words           |
| Local data persistence        | Projects saved with autosave, reliable crash recovery                   |
| Export                        | PDF/ePub/DOCX/HTML export with formatting                               |
| Responsive UI                 | Works on Windows, macOS, Linux; theme support                           |
| AI-powered assistant          | Contextual suggestions, summaries, and creative tools via OpenRouter    |

---

## 3. Personas & Use Cases

- **Indie Novelist:** Manages multiple books, needs easy navigation, formatting, export, and AI brainstorming.
- **Editor/Coach:** Reviews projects, summarizes chapters, uses AI to suggest edits.
- **Game Writer:** Manages assets, uses AI for quick outline/dialogue ideas.

---

## 4. Information Architecture

```
/UserData/NovelStudio/
├── /Projects/
│   ├── [ProjectId]/
│   │   ├── /Chapters/
│   │   │   ├── [ChapterId].json
│   │   ├── /Characters/
│   │   ├── /Notes/
│   │   ├── metadata.json
│   │   └── settings.json
└── appsettings.json
```

---

## 5. High-Level System Architecture

| Layer            | Responsibilities                                  | Technologies                                       |
|------------------|--------------------------------------------------|----------------------------------------------------|
| UI               | Layout, panels, dialogs, navigation               | Avalonia, XAML, .NET 8, MVVM (Prism/Toolkit)       |
| Editor           | Rich text editing, formatting, spellcheck         | Avalonia.Controls.RichTextBox, NHunspell/LanguageTool.NET |
| State Management | App/project state, user settings                  | MVVM, ObservableObject, DI/IoC                     |
| Persistence      | Local file IO, autosave, import/export            | .NET IO, Newtonsoft.Json/YamlDotNet                |
| Export           | Formatting, conversion                            | Pandoc CLI, Calibre CLI, PDF libraries             |
| Source Control   | Git operations                                    | LibGit2Sharp                                       |
| AI Assistant     | Brainstorming, suggestions, summaries             | OpenRouter API (HTTP), C# HttpClient               |

---

## 6. Key Functional Components

1. **Project Explorer:** Tree view (books, chapters, scenes); drag & drop, context menus.
2. **Tabbed Editor Area:** Multi-tab, rich text editing, undo/redo, spellcheck.
3. **Character & Note Sheets:** Structured records with easy editing.
4. **Export Dialog:** PDF, ePub, DOCX, HTML export; choose book/chapters.
5. **Settings:** Theme, font size, AI/LLM opt-in, privacy.
6. **AI Assistant Panel:**  
   - Sidebar or floating panel powered by OpenRouter LLM.  
   - Features: brainstorming, outline generation, character/dialogue suggestions, tone/style checks, summaries, and “Ask AI” for any prompt.  
   - User selects text or provides prompt, receives suggestions, and can insert/replace in editor.  
   - All LLM requests are user-initiated and processed securely.

---

## 7. User Experience & Layout

```
┌──────────────────────────────────────────────────────────────────────────┐
│ Menu  | Toolbar                                                         │
├───────┬─────────────────────────────┬────────────┬───────────┬──────────┤
│Sidebar│   Editor Tabs (RichText)    │ Characters │  Notes    │ AI Panel │
│(Tree) │   Rich Text Editor(s)       │/Outline    │/Timeline  │          │
├───────┴─────────────────────────────┴────────────┴───────────┴──────────┤
│ Status Bar: autosave ● wordcount ● caret pos ● theme ● AI status        │
└──────────────────────────────────────────────────────────────────────────┘
```
- All panes resizable/dockable.  
- AI panel can be opened/closed.

---

## 8. Data & File Formats

| Data             | Format           |
|------------------|-----------------|
| Project Metadata | JSON             |
| Chapters/Scenes  | Rich text (XAML/RTF/JSON) |
| Characters/Notes | JSON             |
| Exports          | DOCX, PDF, HTML, ePub |
| AI Prompts/Responses | Text/JSON (temp/session only) |

---

## 9. Dependencies

- **.NET 8 + Avalonia**
- **Prism** or **CommunityToolkit.Mvvm**
- **LibGit2Sharp** (Git integration)
- **NHunspell** / **LanguageTool.NET** (spellcheck)
- **Pandoc/Calibre CLI** (export)
- **Newtonsoft.Json/YamlDotNet** (data serialization)
- **OpenRouter LLM API** (AI writing support)

---

## 10. Non-Functional Requirements

| Aspect        | Target                                        |
|---------------|-----------------------------------------------|
| Performance   | Load 50+ chapters ≤ 2s                        |
| Reliability   | Autosave every 10s/on edit, crash recovery    |
| Accessibility | Keyboard nav, font scaling, high-contrast     |
| Security      | All data local unless user opts in to AI      |
| Privacy       | AI features opt-in; user must enable/authorize|

---

## 11. Future Extensions

- Cloud sync (optional, e.g., OneDrive/Dropbox)
- Comments/inline annotation
- Version history, branching, merges (Git)
- Real-time collab (SignalR or WebRTC)
- Expanded AI: genre, style, workflow chains

---