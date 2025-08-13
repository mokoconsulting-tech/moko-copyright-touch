<!--
Copyright (C) 2025 Jonathan Andrew Miller || Moko Consulting <hello@mokoconsulting.tech>

This file is part of the moko-copyright-touch project.

moko-copyright-touch is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

moko-copyright-touch is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with moko-copyright-touch. If not, see <https://www.gnu.org/licenses/>.
-->

# moko-copyright-touch — DOCUMENTATION.md

Copyright 2025 Moko Consulting. Licensed under the GNU General Public License v3.0 or later (GPL-3.0-or-later). You may redistribute and/or modify this documentation under the terms of the GPL as published by the Free Software Foundation.

> Comprehensive reference for configuring, running, and extending **moko-copyright-touch**, a tool that applies or updates standardized, Doxygen-compatible copyright headers across source files.

---

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [Runtime Flags (CLI)](#2-runtime-flags-cli)
3. [Behavior & Logic](#3-behavior--logic)
4. [Project Parameters File](#4-project-parameters-file--moko-copyright-touchparamsjson)
5. [Default Configuration File](#5-default-configuration-file--moko-copyright-touchdefaultjson)
6. [Placeholder Glossary](#6-placeholder-glossary)
7. [Header Templates File](#7-header-templates-file--moko-copyright-touch-headertemplatejson)
8. [Supported File Types & Comment Styles](#8-supported-file-types--comment-styles)
9. [Examples (Rendered)](#9-examples-rendered)
10. [Detection Heuristics (Technical)](#10-detection-heuristics-technical)
11. [FAQ](#11-faq)
12. [Conventions & Recommendations](#12-conventions--recommendations)

---

## 1) Quick Start

```bash
# Dry-run (default)
./moko-copyright-touch.ps1 --startin "." --dryrun:true

# Write changes to disk
./moko-copyright-touch.ps1 --startin "." --apply --dryrun:false
```

* Reads `moko-copyright-touch.params.json` and `moko-copyright-touch-headertemplate.json` from the **project root**.
* Falls back to the **script directory** if not found.
* Inserts a new header **after a shebang** if present.
* Prompts for missing values unless `--noninteractive` is set.

---

## 2) Runtime Flags (CLI)

| Flag                        | Type      | Default                         | Description                                                  |
| --------------------------- | --------- | ------------------------------- | ------------------------------------------------------------ |
| `--startin`                 | string    | `"."`                           | Root folder to scan.                                         |
| `--apply` / `-Apply`        | switch    | `false`                         | Apply changes to disk.                                       |
| `--dryrun`                  | bool      | `true`                          | Preview actions without writing.                             |
| `--noninteractive`          | switch    | `false`                         | Disable interactive prompts.                                 |
| `--params`                  | string    | *(auto)*                        | Path to params JSON.                                         |
| `--templates`               | string    | *(auto)*                        | Path to headertemplate JSON.                                 |
| `--include`                 | string\[] | all supported                   | Glob(s) to include (`,` separated).                          |
| `--exclude`                 | string\[] | none                            | Glob(s) to exclude.                                          |
| `--force`                   | switch    | `false`                         | Force overwrite even if a non-standard header exists.        |
| `--update-existing`         | switch    | `true`                          | Update recognized headers in place.                          |
| `--skip-if-any-top-comment` | switch    | `false`                         | If any top-of-file comment exists, skip insertion.           |
| `--backup`                  | switch    | `true`                          | Save `*.bak` before modifying files.                         |
| `--log`                     | string    | `./logs`                        | Directory for run logs.                                      |
| `--license-url`             | string    | `https://www.gnu.org/licenses/` | License URL to embed when applicable.                        |
| `--encoding`                | string    | `utf-8`                         | Encoding used when writing files.                            |
| `--newline`                 | enum      | `auto`                          | `auto`, `lf`, or `crlf`.                                     |
| `--year`                    | string    | *(auto)*                        | Override computed `{{Years}}` (e.g., `2025` or `2021-2025`). |
| `--simulate-file`           | string    | none                            | Resolve and preview a single filename against templates.     |

---

## 3) Behavior & Logic

1. **Scan**: Walk `--startin`, apply `--include`/`--exclude` globs.
2. **Detect**: Search for a recognized header via sentinels (SPDX/GNU wording/`@defgroup`).
3. **Update vs Insert**: If found and `--update-existing` is true, update in place; otherwise insert a new header at the top (after shebang).
4. **Comment Style**: Choose delimiters based on file type (block/line/html/markdown/hash).
5. **Template Selection**: Match by extension; otherwise fall back to the `default` block.
6. **Years**: Derive from VCS (first commit → current year) or system year, unless `--year` is provided.
7. **Safety**: Create backups if `--backup`; respect `--dryrun`.

---

## 4) Project Parameters File — `moko-copyright-touch.params.json`

```json
{
  "holder": "",
  "email": "",
  "phone": "",
  "spdx": "",
  "defgroup": "",
  "ingroup": "",
  "brief": "",
  "description": "",
  "projectname": "",
  "include": [],
  "exclude": [],
  "newline": "auto",
  "encoding": "utf-8",
  "license_url": "",
  "update_existing": true,
  "skip_if_any_top_comment": false,
  "backup": false
}
```

---

## 5) Default Configuration File — `moko-copyright-touch.default.json`

```json
{
  "startin": "",
  "destination": "",
  "holder": "",
  "email": "",
  "phone": "",
  "years": "",
  "license": "gpl-3.0-or-later",
  "additionalinfo": false,
  "wordwrap": 40,
  "includesubdirectories": true,
  "filetypes": [".php", ".js", ".css", ".html", ".ini", ".xml"],
  "ignorepatterns": [
    "node_modules",
    "vendor",
    "*.min.js",
    "*.min.css",
    "*.map",
    "moko-copyright-touch.params.json",
    "moko-copyright-touch-headertemplate.json"
  ],
  "backupbeforemodify": true,
  "backuplocation": "./.moko-copyright-touch-backups",
  "headertemplate": "",
  "defaultdefgroup": "dolibarr",
  "defaultingroup": "template.moko-cassiopeia",
  "relativefilepathinheader": true,
  "promptformissingvalues": true
}
```

---

## 6) Placeholder Glossary

| Placeholder                     | Description          | Source                                | Notes                                           |
| ------------------------------- | -------------------- | ------------------------------------- | ----------------------------------------------- |
| `{{Years}}`                     | Year or year range.  | VCS or `--year`.                      | Accepts `YYYY-YYYY` ranges.                     |
| `{{Holder}}`                    | Copyright holder.    | `holder` param/default.               | Required for most use cases.                    |
| `{{Email}}`                     | Contact email.       | `email` param/default.                | Optional.                                       |
| `{{Phone}}`                     | Contact phone.       | `phone` param/default.                | Optional.                                       |
| `{{License}}`                   | SPDX license ID.     | `spdx`/`license`.                     | e.g., `gpl-3.0-or-later`, `mit`.                |
| `{{DefGroup}}`                  | Doxygen `@defgroup`. | `projectname` if set else `defgroup`. | Default `dolibarr`.                             |
| `{{Brief}}`                     | One-line summary.    | `brief`.                              | Keep concise.                                   |
| `{{FileName}}`                  | File path/name.      | Computed from file.                   | Relative if `relativefilepathinheader` is true. |
| `{{InGroup}}`                   | Doxygen `@ingroup`.  | `ingroup`.                            | Default `template.moko-cassiopeia`.             |
| `{{Description}}`               | Multi-line details.  | `description`.                        | Wrapped to `wordwrap` width.                    |
| `{{ProjectName}}`               | Project name.        | `projectname`.                        | Overrides `DefGroup` if set.                    |
| `{{TAB}}`/`{{TAB2}}`/`{{TAB4}}` | Indentation units.   | Template `tab_char`/`tab_size`.       | Aligns long lines.                              |

---

## 7) Header Templates File — `moko-copyright-touch-headertemplate.json`

The templates file defines **per-extension** blocks and an optional global `default` block.

### Structure

* `comment_style`: `block` | `line` | `html` | `markdown` | `hash`
* `block_start`, `block_line_prefix`, `block_end`: for `block` style
* `line_prefix`: for `line` style
* `html_start`, `html_end`: for `html` style
* `tab_char`: character for one indentation unit (default `"\t"`)
* `tab_size`: spaces to use when expanding a tab unit (default `4`)
* `content`: array of header lines with placeholders

### Selection Logic

* Choose template by extension; if none matches, use `default`.
* TAB placeholders (`{{TAB}}`, `{{TAB2}}`, `{{TAB4}}`) expand using `tab_char`/`tab_size`.

### Example File Using All Variables

```json
{
  "php": {
    "comment_style": "block",
    "block_start": "/*",
    "block_line_prefix": " * ",
    "block_end": " */",
    "tab_char": "\t",
    "tab_size": 4,
    "content": [
      "Copyright (C) {{Years}} {{Holder}} <{{Email}}> | {{Phone}}",
      "SPDX-License-Identifier: {{License}}",
      "@defgroup {{DefGroup}}",
      "@brief {{Brief}}",
      "@file {{FileName}}",
      "@ingroup {{InGroup}}",
      "Project: {{ProjectName}}",
      "{{Description}}",
      "License URL: ${license_url}",
      "Tab: {{TAB}}{{Brief}}",
      "Tab2: {{TAB2}}{{Description}}",
      "Tab4: {{TAB4}}End"
    ]
  },
  "default": {
    "comment_style": "line",
    "line_prefix": "# ",
    "tab_char": "\t",
    "tab_size": 4,
    "content": [
      "Copyright (C) {{Years}} {{Holder}} <{{Email}}>",
      "SPDX-License-Identifier: {{License}}",
      "@brief {{Brief}}",
      "@file {{FileName}}"
    ]
  }
}
```

> Note: `${license_url}` is interpolated from the params file when present.

---

## 8) Supported File Types & Comment Styles

| Extensions  | Style    | Start       | Prefix | End   |
| ----------- | -------- | ----------- | ------ | ----- |
| php         | block    | `/*`        | `*`    | `*/`  |
| js, ts, css | block    | `/*`        | `*`    | `*/`  |
| html, htm   | html     | `<!--`      | ` `    | `-->` |
| md          | markdown | `[//]: # (` |        | `)`   |
| py, sh, ini | hash     |             | `# `   |       |

---

## 9) Examples (Rendered)

### PHP

```php
/*
 * Copyright (C) 2023-2025 [Your Organization or Name] <your-email@example.com> | [optional-phone-number]
 * SPDX-License-Identifier: gpl-3.0-or-later
 * @defgroup dolibarr | @ingroup template.moko-cassiopeia
 * @brief Project-wide copyright header
 * @file path/to/file.php
 * Standardized header for all project files.
 */
```

### Markdown (invisible)

```md
[//]: # (
Copyright (C) 2025 [Your Organization or Name] <your-email@example.com>
SPDX-License-Identifier: gpl-3.0-or-later
@defgroup dolibarr | @ingroup template.moko-cassiopeia
@brief Project-wide copyright header
@file path/to/README.md
)
```

---

## 10) Detection Heuristics (Technical)

* Recognize headers by any of:

  * `SPDX-License-Identifier:` line
  * GNU disclaimer phrases ("This program is free software…")
  * Doxygen markers (`@defgroup`, `@ingroup`)
* Insert **after shebang** if present.
* Respect `--skip-if-any-top-comment` when enabled.

---

## 11) FAQ

**How are years computed?** From VCS history or current year; override with `--year`.

**Can I add a new file type?** Yes, add a block in the headertemplate JSON with the appropriate `comment_style` and delimiters.

**How do I prevent changes to custom headers?** Enable `skip_if_any_top_comment` or run without `--update-existing`.

**Does it work without Git?** Yes—defaults to current year.

**Can I use multiple licenses?** Yes—use a valid SPDX expression (e.g., `gpl-3.0-or-later OR mit`).

**What happens if placeholders are missing values?** The script will prompt for missing parameters unless `--noninteractive` is set, in which case they will be left blank or use defaults.

**How does it handle files with a shebang line?** The header will be inserted after the shebang to preserve script execution behavior.

**Can I disable backups?** Yes—set `backup` to false in params or pass `--backup:false` on the CLI.

**Will it reformat my code?** No—the tool only prepends or updates the header, leaving the rest of the file unchanged.

**How do TAB placeholders work?** They expand to the configured `tab_char` or spaces according to `tab_size` in the template block.

---

## 12) Conventions & Recommendations

* Prefer SPDX identifiers for license lines.
* Keep templates succinct and consistent across languages.
* Tune `tab_char`/`tab_size` per language for neat alignment.
* Use markdown comment fences for `.md` files to keep headers invisible in renderers.

---