# LazyBug - Visual Studio AI Coding Assistant Extension

[![Visual Studio Marketplace](https://img.shields.io/badge/VS%20Marketplace-Install-blue?logo=visual-studio)](https://marketplace.visualstudio.com/items?itemName=IxSoftware.lazybug2026)
[![Version](https://img.shields.io/badge/version-0.18.1-blue)](https://github.com/ixnehc/LazyBug-Copilot-Publish/blob/main/patchnotes.md)
[![Visual Studio 2022](https://img.shields.io/badge/Visual%20Studio-2022-purple?logo=visual-studio)](https://marketplace.visualstudio.com/items?itemName=IxSoftware.lazybug2026)

## Product Overview

LazyBug is a "Cursor-like" intelligent coding assistant extension designed specifically for Visual Studio. It integrates Large Language Model (LLM) capabilities to provide developers with intelligent code creation, refactoring, and Q&A experiences. The extension supports multiple mainstream AI service providers, enabling developers to enjoy AI-assisted programming within their familiar IDE environment.

![screenshot](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/screenshot.gif)

---

## Version 0.19 Release Notes

**Features**

- Added MCP support (stdio and URL)
- Added a UI to manage MCPs
- Added cache rate in the cost statistics label

**Bug Fixes**

- Fix an issue that sometimes the reasoning_content is not correctly sent back to LLM for Kimi and DeepSeek, which results in significant performance degrade in complex tasks
- Fix a potential crash when outputing log.
- Disabled the bash tool when bash is not available on current system
- Enabled streaming tool calls for the GLM API
- Fixed an issue where starting a new conversation after rolling back all previous conversations would reset the chat title
- Fixed an issue where the chat input window could not regain focus when the Visual Studio window was brought back to the foreground
- Restored the cursor to its previous position after the chat input window regains focus
- Fixed an issue where token statistics would become excessively large when using certain endpoints
- Fixed an issue that finding keywords in files will fail when the files are too big

_See [patchnotes.md](https://github.com/ixnehc/LazyBug-Copilot-Publish/blob/main/patchnotes.md) for full version history._

---

## Core Features

- **Multi-Turn Intelligent Chat** — Markdown-based chat content. Session history stored per VS solution.
- **Symbol Link Recognition** — Clickable symbol links in the chat window for quick navigation to definitions.
- **Smart Code Editing** — AI directly modifies project files with multi-file support, before/after Diff View, modification tracking, undo/redo , and file backup.
- **Codebase Search** — Fast text and symbol search for ultra-large projects (million-line scale, C/C++/C#). Text search is significantly faster than ripgrep, especially in large codebases. Symbol search works out of the box — no LSP configuration required. AI automatically reads related files for context.
- **Smart Input Box** — Tag-based file attachment system with `@` auto-completion, input history (`PageUp`/`PageDown`), quick model switching, and direct image paste.

![chatinput](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/chatinput.jpg)
![image support](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/image_support2.jpg)

- **Multi-Model Support** — Built-in providers: OpenAI, Anthropic, Google Gemini, OpenRouter, Moonshot (Kimi), z.ai (GLM), DeepSeek. Supports custom API endpoints and local LLMs (Ollama, LM Studio).
- **Multi-API Format** — Supports three API formats: OpenAI-compatible, Anthropic, and Gemini.

![provider](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/provider.jpg)

- **Skill System** — Browse, create, rename, and toggle skills via a management panel. Supports BuiltIn, Global, and Project-level skills. Use AI to edit or create new skills.

![skill](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/skill.jpg)

- **Custom Prompts** — `global_rules.txt` and `project_rules.txt` for customized prompts; `cli_whitelist.ini` for trusted CLI commands.

![settings](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/settings2.jpg)

- **CLI Tool Integration** — Execute cmd.exe, bash.exe, python.exe scripts directly from the chat, extending capabilities beyond coding.

![output](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/output_10fps.gif)

- **Context Usage Control** — Real-time context usage display with 5 context levels. Allow keeping context under relatively low level (<30k tokens) even in extremely long conversations while maintaining high response quality. Automatic compression/decompression when context level changes.

![contextlevel](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/contextlevel.jpg)

- **MCP Support** — Model Context Protocol support via stdio and URL, with a built-in UI to manage MCP servers.

![mcp](https://github.com/ixnehc/LazyBug-Copilot-Publish/raw/main/screenshots/createmcp.gif)
- **Session Management** — Switch between historical sessions, one-click rollback to any previous state, favorites management, and cost statistics per session.
- **Image Attachment** — Paste images directly into the chat input to send to vision-capable LLMs.
- **UI Scaling** — Hold `Ctrl` and scroll to freely zoom the chat interface and text size.



## Usage Scenarios

- **Code Review and Refactoring**: Let AI analyze your code and suggest refactoring improvements.
- **New Feature Development**: Describe your requirements, and AI will assist in generating code frameworks and implementations.
- **Bug Fixing**: Describe the issue symptoms, and AI will help locate and fix the bug.
- **Code Explanation**: Ask about complex code logic, and AI will provide detailed explanations.

---

## Usage Tips

- **Open the Chat Panel**: Open the chat panel via the Visual Studio menu `View` → `Other Windows` → `LazyBug Chat`. It is recommended to bind a shortcut to the `View.LazyBugChat` command for quick access.
- **Database and Disk Space**: The LazyBug chat database is independent of the project and is stored centrally on the C drive. Please ensure sufficient free space on your C drive (for ultra-large projects, more than 10 GB may be required).
- **Adding File Attachments**:
  - Select a file in the **Solution Explorer**, right-click, and choose **Add to LazyBug Chat** to attach it to the current conversation.
  - You can also do the same by right-clicking the file's tab above the code editor.
- **Symbol Database Construction (C/C++)**: When you open a C/C++ project for the first time, LazyBug will automatically build the symbol database in the background. For ultra-large projects (e.g., 3 million lines of code), this process may take a significant amount of time (approximately 30 minutes to 1 hour). Symbol query results may not be fully accurate until the build is complete.
- **Code Comparison (Diff View)**:
  - Click the title of a file editing label in the chat panel to display the Diff view in the main editor; press `Space` to hide it.
  - Clicking the title repeatedly allows you to quickly jump between different diff hunks.
- **Avoid Editing Conflicts**: Please do not manually edit files while AI is working, especially when it is modifying file contents.
- **UI Scaling**: When the mouse focus is inside the LazyBug chat window, hold `Ctrl` and scroll the mouse wheel to freely zoom the interface and text size.
- **Cost Statistics**: The cost for each chat turn is calculated based on the unit price entered in the LLM api setting. When the LLM provider uses a complex billing model (such as a subscription plan), the statistics are approximate and for reference only.
- **Task Breakdown Strategy**: LazyBug is not designed to handle extremely large and complex tasks in a single pass. Break your development tasks into smaller, clearly defined sub-tasks for the best AI-assisted experience.
- **Code Database Updating**: After adding a new file to the solution, save the solution file so that the new file is included in the code database.
- **Skill Usage**:
  - There are 3 types of skills:
    - **BuiltIn**: Verified skills bundled with the extension. These should generally not be modified.
    - **Global**: Skills shared across all projects.
    - **Project**: Skills specific to the currently opened project.
  - Activating a skill does not mean its full content is loaded into the context. To force-load a skill, copy its path and paste it into the file attachment list.
  - Many existing skills exist in the ecosystem and may have compatibility issues with LazyBug. You may need to tweak them until they work smoothly.
  - You are always encouraged to use AI to edit existing skills or create new ones.
  - Install the necessary environments (Node.js, Python, GIT, etc.) to support various CLI commands.
- **Context Level Settings**:
  - Higher context levels consume more tokens and incur higher costs, especially on expensive models.
  - However, higher context levels reduce the frequency of compression, which improves cache hit rates and can also lower costs to some extent.
  - Currently, context is not compressed within a single Q&A turn to avoid cache miss.
  - Compression is not unlimited — it will always preserve a baseline answer quality. So even if you set a low context level, sometimes context usage may still significantly exceed the upper limit.
  - That said, compression will more or less degrade the model's answer quality.
  - **Overall recommendation**: For expensive models (Anthropic, GPT), set the lowest context level (<30k tokens), unless you notice a significant drop in answer quality.

---

## Contact Us

If you encounter any bugs or have suggestions for improvement, please feel free to reach out via email. Your feedback is the driving force behind our continuous improvement!

- 📧 **Contact Email**: [ixnehc1974@gmail.com](mailto:ixnehc1974@gmail.com)
