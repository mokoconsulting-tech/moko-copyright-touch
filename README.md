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
# moko-copyright-touch - README.md

**moko-copyright-touch** is a lightweight, configurable script that automatically applies or updates standardized, **Doxygen-compatible** copyright headers to source files.

---

## 📋 Features

* **Automatic header insertion and update**
  Detects existing headers in a known format and updates them; otherwise inserts a new one.

* **JSON-based defaults**
  Loads parameters from `moko-copyright-touch.params.json` in the project root (or script folder if missing).

* **Parameter fallbacks**
  Project parameters override script defaults; CLI overrides both.

* **Interactive prompting**
  Prompts for missing parameters and writes them to the params file.

* **Flexible configuration**
  Supports multiple programming languages with proper comment styles. Default `@defgroup` is `dolibarr` unless overridden.

* **Header templates**
  Use `headertemplate` JSON files to define reusable headers for one or multiple file types. Supports grouped targets via comma-separated keys or `apply_to` arrays. Falls back to the `php` template if no match is found.

* **Shortcut-friendly**
  `startin` can be set for running from shortcuts.

* **Self-healing defaults**
  If no params file is found, one is created with supplied or prompted defaults.

---

## 📑 Full Documentation

All parameter definitions, placeholder references, and header template rules are located in:

**[DOCUMENTAION.md](./DOCUMENTAION.md)**

---

## 🚀 Usage

**Basic run:**

```bash
moko-copyright-touch <file-or-directory>
```

**With flags:**

```bash
moko-copyright-touch <target> --verbose --skip-existing
```

**Runtime flags:**

* `--dry-run` – Show changes without modifying files.
* `--verbose` – Detailed log output.
* `--force` – Overwrite existing headers.
* `--skip-existing` – Skip files with any existing comment header.

---

## 🛠 License

Licensed under the GNU General Public License v3.0 or later.

© 2025 Moko Consulting. All rights reserved.
