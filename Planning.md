# NovelStudio Planning

## Vision & Scope

A cross-platform desktop rich text writing app for authors, with easy project/scene management, character/notes support, offline access, and export to PDF/ePub/DOCX/HTML. Built-in, optional AI writing assistant (OpenRouter LLM) offers brainstorming, suggestions, and creative tools—privacy-focused, opt-in.

---

## Release Strategy

- **MVP:**
  - Project/chapter/scene management
  - Rich text editor
  - Local file storage & autosave
  - Export as DOCX/PDF/ePub
- **v1.0:**
  - Multi-tab editor, drag-and-drop navigation
  - Characters, notes, search
  - Settings panel (theme/font, autosave, privacy)
  - AI assistant sidebar (OpenRouter) for prompts, suggestions, summaries
  - Accessibility polish
- **Post-1.0:**
  - Version history
  - Inline comments
  - Plugins/extensions
  - Cloud sync (opt-in)
  - Expanded AI workflows

---

## Major Milestones

**Phase 1: Foundation**
- .NET 8 + Avalonia project setup
- Project explorer, file CRUD, local save/load
- Basic editor with rich text

**Phase 2: Authoring & Organization**
- Formatting toolbar, keyboard shortcuts, multi-tab
- Drag-and-drop chapters/scenes
- Characters, notes

**Phase 3: Data Management**
- Search, outline panel
- Export dialog (DOCX, PDF, ePub, HTML)

**Phase 4: AI Integration**
- OpenRouter API integration
- AI Assistant panel UI/UX
- Prompt/response workflow
- Settings for AI opt-in/privacy

**Phase 5: QA/Polish**
- Accessibility
- Final bugfix/QC
- Documentation

---

## Technical Stack

- **.NET 8, Avalonia, XAML, MVVM**
- **LibGit2Sharp**
- **NHunspell/LanguageTool.NET**
- **Pandoc/Calibre CLI**
- **OpenRouter API (LLM, HTTP)**

---

## Risks & Mitigations

- API limits or downtime → graceful error, retry, fallback
- Large project memory use → async load, virtualization
- AI misuse/privacy → clear opt-in, local-only by default

---

## Roadmap Summary

| Phase   | Major Deliverables                        |
|---------|-------------------------------------------|
| 1       | Shell, sidebar, basic editor, local save  |
| 2       | Formatting, tabs, drag-and-drop           |
| 3       | Characters, notes, search, export         |
| 4       | AI assistant panel, OpenRouter integration|
| 5       | Accessibility, polish, QA                 |