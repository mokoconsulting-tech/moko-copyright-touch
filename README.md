# README.md

**moko-copyright-touch** is a lightweight, configurable script that automatically applies or updates standardized, **Doxygen-compatible** copyright headers to source files.

---

## 📋 Features

* **Automatic header insertion and update** – Detects existing headers in a known format and updates them; otherwise, inserts a new one.
* **JSON-based defaults** – Loads parameters from `moko-copyright-touch.params.json` in the project root (or script folder if missing).
* **Parameter fallbacks** – Project parameters override script defaults; CLI overrides both.
* **Interactive prompting** – Prompts for missing parameters and writes them to the parameters file.
* **Flexible configuration** – Supports multiple programming languages with proper comment styles. Default `@defgroup` is `dolibarr` unless overridden.
* **Header templates** – Use `headertemplate` JSON files to define reusable headers for one or multiple file types. Supports grouped targets via comma-separated keys or `apply_to` arrays. Falls back to the `php` template if no match is found.
* **Shortcut-friendly** – `startin` can be set for running from shortcuts.
* **Self-healing defaults** – If no parameters file is found, one is created with supplied or prompted defaults.
* **Multi-file type application** – Apply HTML or other header templates to multiple file types at once.
* **SPDX license integration** – Add standardized SPDX license identifiers automatically.

---

## 📦 Installation

1. **Clone the repository:**

```bash
git clone https://github.com/mokoconsulting-tech/moko-copyright-touch.git
```

2. **Navigate into the project folder:**

```bash
cd moko-copyright-touch
```

3. **Make the script executable** (Linux/macOS):

```bash
chmod +x moko-copyright-touch
```

4. **(Optional)** Add the script to your PATH for global usage:

```bash
export PATH="$PATH:$(pwd)"
```

5. **(Optional)** Create a `moko-copyright-touch.params.json` file in the script folder (or copy and modify the example from the `templates` folder) to set default parameters.
   If this file is not present, the script will prompt for all default parameters during the first run and save them automatically.

---

## 📑 Full Documentation

Full details on parameters, placeholders, and header template configuration are available in:

**[DOCUMENTATION.md](./DOCUMENTATION.md)**

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
* `--apply-to-all` – Apply a header template to all supported file types.

---

## 👨‍💻 Developer

**Jonathan Miller**
Moko Consulting
📧 [dev@mokoconsulting.tech](mailto:dev@mokoconsulting.tech)

---

## 🛠 License

Licensed under the GNU General Public License v3.0 or later. See [LICENSE](LICENSE) for details.

© 2025 Moko Consulting. All rights reserved.
