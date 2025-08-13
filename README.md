# moko-copyright-touch - README.md

**moko-copyright-touch** is a lightweight, configurable script that automatically applies or updates standardized, Doxygen-compatible copyright headers to source files across multiple languages. It supports reading configuration from JSON, overriding via CLI or shortcuts, and prompting for missing values.

## 📋 Features

* **Automatic header insertion and updating** – Inserts a GPL or other configured license header if missing, or updates an existing matching-format header.
* **Header update detection** – Detects existing headers in a known or matching format and updates them with the latest configuration values.
* **JSON-based configuration** – Reads defaults from `moko-copyright-touch.params.json` in the project root or script folder.
* **Parameter fallbacks and prompts** – Project values override script defaults; any missing values are prompted for and saved.
* **Header templates** – Loads from the `templates/` directory; supports multiple file types and comment styles, including sample JSON structures for special files.
* **Backup system** – Optionally creates backups before modifying files, with a configurable backup location.
* **Shortcut and CLI overrides** – Flexible parameter control from desktop shortcuts or direct CLI input.
* **Self-healing defaults** – Creates a new params file on first run if none is found, populated from prompts or CLI.
* **Merge logic** – Ensures project-specific settings take precedence, with script-level defaults and CLI parameters layered in.

## 📂 Default JSON Structure

```json
{
  "StartIn": "",
  "Destination": "",
  "Holder": "",
  "Email": "",
  "Phone": "",
  "Years": "",
  "License": "",
  "AdditonalInfo": false,
  "wordwrap": 40,
  "IncludeSubdirectories": true,
  "FileTypes": [".php", ".js", ".css", ".html", ".ini", ".xml"],
  "IgnorePatterns": [
    "node_modules",
    "vendor",
    "*.min.js",
    "*.min.css",
    "*.map",
    "moko-copyright-touch.params.json",
    "moko-copyright-touch.headertemplates.json"
  ],
  "BackupBeforeModify": true,
  "BackupLocation": "./.moko-copyright-touch-backups",
  "HeaderTemplate": "",
  "DefaultDefGroup": "Dolibarr",
  "DefaultInGroup": "Template.moko-cassiopeia",
  "RelativeFilePathInHeader": true,
  "PromptForMissingValues": true
}
```

## Documentation
 [Default Configuration Reference](./DOCUMENTAION.md).

## 🧠 Behavior & Merge Logic

1. Load project-level `moko-copyright-touch.params.json` (if present).
2. Load script-level `moko-copyright-touch.params.json` (fallback defaults).
3. Merge: project values override script defaults.
4. Apply CLI/shortcut overrides last.
5. Prompt for any remaining missing parameters and save to the params file.
6. Apply the selected header template from `templates/`.
7. If an existing header matches a known format, update it in place rather than inserting a duplicate.

## 🔧 Supported File Types

* PHP, JS, CSS, HTML, XML, INI, SQL, SH, and more — each with matching comment styles.

## 🛡 License

Licensed under the GNU General Public License v3.0 or later. See [GNU Licenses](https://www.gnu.org/licenses/).

## 👤 Developer

**Jonathan Miller**
📧 [dev@mokoconsulting.tech](mailto:dev@mokoconsulting.tech)
🌐 [https://mokoconsulting.tech](https://mokoconsulting.tech)
