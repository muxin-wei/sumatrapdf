# SumatraPDF with AI Copilot & Modeless Translation

[![Build](https://github.com/sumatrapdfreader/sumatrapdf/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/sumatrapdfreader/sumatrapdf/actions/workflows/build.yml)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

---

## Key Features

- **Selection Translation**  
  ![Selection Translation](docs/images/selection-translate.png)  
  *A Chrome-style non-blocking floating bubble opens directly next to selected paper passages for instant translation without obscuring the reading flow or launching external browser tabs.*

- **Multi-Engine AI Chat & Document Assistant**  
  ![AI Chat & Document Assistant](docs/images/ai-chat-assistant.png)  
  *Select complex academic formulas, equations, or dense paragraphs to trigger contextual derivation and in-depth explanations in the AI sidebar with offline KaTeX math rendering.*

- **Decoupled Model Selection & Reasoning Effort**  
  ![Decoupled Model Selection & Reasoning Effort](docs/images/model-effort-decoupled.png)  
  *Model selection and thinking effort are separated into independent controls (`Low`, `Medium`, `High`, `Disabled`), eliminating CLI flag conflicts and allowing granular control over reasoning depth.*

- **Isolated Agent Sessions & Anti-Pollution**  
  ![Isolated Agent Sessions & Anti-Pollution](docs/images/session-isolation.png)  
  *Agent CLI invocations run under isolated `--project sumatrapdf` workspaces and document-scoped session IDs, ensuring reading queries never clutter your primary terminal logs.*

---

## Configuration Reference

Edit `SumatraPDF-settings.txt` (or via **Settings -> Advanced Options**):

```txt
AiChat [
	Enabled = true
	Provider = antigravity     # Options: gemini, antigravity, claude, codex, grok
	Model = gemini-2.5-flash
	Effort = medium            # Options: low, medium, high, disabled
	ApiKey =                   # For direct Gemini REST API
	AutoApprove = true
	TranslateLanguage = zh-CN  # Default translation target
]

SelectionTranslate [
	Enabled = true
	AutoPopup = false          # Show bubble immediately on selection
	DefaultTargetLang = zh-CN
	Pinned = false
]
```

---

## Building from Source

### Prerequisites
- Visual Studio 2022 / Build Tools (with C++ Desktop workload)
- Node.js (for asset preparation)
- Git

### Build Steps

1. **Clone the repository:**
   ```cmd
   git clone https://github.com/muxin-wei/sumatrapdf.git
   cd sumatrapdf
   ```

2. **Pack embedded offline assets (KaTeX & UI scripts):**
   ```cmd
   cmd\pack-embedded-prebuild.cmd
   ```

3. **Compile Release x64 binary:**
   ```cmd
   call "C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build\vcvarsall.bat" x64
   msbuild /m /p:Configuration=Release /p:Platform=x64 vs2022\SumatraPDF.sln
   ```

The compiled binaries will be generated under `out\rel64\SumatraPDF.exe` and `out\rel64\libsumatrapdf.dll`.

---

## License

SumatraPDF is released under the **GNU General Public License v3 (GPLv3)**. Some third-party subcomponents are distributed under BSD or MIT licenses (see [AUTHORS](AUTHORS)).
