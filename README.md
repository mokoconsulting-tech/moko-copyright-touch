# moko-copyright-touch

**moko-copyright-touch** is a lightweight, configurable script that automatically applies a standardized copyright header to source files. It supports pulling default metadata from a JSON configuration file, overriding parameters via shortcut or CLI arguments, and prompting the user when missing variables are detected.

---

## 📋 Features

* **Automatic Header Insertion**
  Adds a GNU GPL (or other configured) copyright header to source files that do not already contain one.

* **JSON-Based Defaults**
  Loads default values from `moko-copyright-touch.json` in either the script folder (global defaults) or the project folder (project-specific overrides).

* **Parameter Fallbacks**
  Missing project-level variables are automatically inherited from script-level defaults.

* **Interactive Prompting**
  If no value exists in either file or CLI parameters, the script prompts the user for input.

* **Flexible Configuration**
  Supports multiple programming languages with appropriate comment styles.
  Default `@defgroup` tag is `Dolibarr` unless overridden.

* **Header Templates**
  Supports reusable header templates stored in a `templates` directory. These templates can be customized for different licenses, comment styles, or branding, and selected via JSON or CLI parameters.

* **Shortcut-Friendly**
  Supports a `StartIn` parameter for running via desktop or terminal shortcuts.

* **Self-Healing Defaults**
  If no JSON is found on first run, the script will create one with the supplied or prompted defaults.

---

## 📂 Default JSON Structure

Below is an example of how a default JSON file should be structured.
This can be placed in the **script folder**, so it is used as a fallback for all projects when no project-specific JSON is present, or in the **project folder**, to define parameters for specific projects.

**IT SHOULD ALWAYS HAVE THE NAME `moko-copyright-touch.json`.**

```json
{
  "StartIn": "absolute/path/to/your/project",
  "Destination": "absolute/path/to/your/destination",
  "Holder": "[Your Name] || [Your Organization]",
  "Email": "your-email@example.com",
  "Phone": "your-phone-number",
  "ProjectGroup": "Project",
  "ProjectName": "MyProject",
  "Version": "1.0.0",
  "Years": "2023-2025",
  "License": "GPL-3.0-or-later",
  "AdditionalInfo": false,
  "WordWrap": 40,
  "IncludeSubdirectories": true,
  "FileTypes": [".php", ".js", ".css", ".html", ".ini", ".xml"],
  "IgnorePatterns": ["node_modules", "vendor", "*.min.js", "*.min.css", "*.map", "moko-copyright-touch.json"],
  "BackupBeforeModify": true,
  "BackupLocation": "./.moko-copyright-touch-backups",
  "HeaderTemplate": "HeaderTemplate.default.json",
  "DefaultDefGroup": "Dolibarr",
  "DefaultInGroup": "Template.moko-cassiopeia",
  "RelativeFilePathInHeader": true,
  "PromptForMissingValues": true
}
```

For a detailed explanation of each parameter, see [Default Configuration Reference](/docs/variables.md).

---

## 🚀 Usage

**Basic run:**

```bash
moko-copyright-touch <file-or-directory>
```

**Using shortcut defaults:**

* Create a shortcut with the `StartIn` parameter set.
* The script will auto-load configuration from `moko-copyright-touch.json`.

**Override defaults via CLI:**

```bash
moko-copyright-touch src/ --ProjectName "NewName" --License "MIT"
```

**Using a specific header template:**

```bash
moko-copyright-touch src/ --Template "gpl-block"
```

---

## 🧠 Behavior & Merge Logic

1. Load project-level `moko-copyright-touch.json` (if present).
2. Load script-level `moko-copyright-touch.json` (fallback defaults).
3. Merge: project values override script defaults.
4. Apply CLI/shortcut overrides last.
5. For any parameter still missing, prompt the user.
6. If a template is specified, load it from the `templates` directory and apply it with the resolved variables.

---

## 🔧 Supported File Types & Comment Styles

* **PHP / C / C++ / Java / JS**: block comments `/* ... */` with `*` prefix lines.
* **Python / Shell / YAML**: line comments with `#`.
* **HTML / XML**: `<!-- ... -->`.
* **INI / Properties**: `;` or `#` lines.

> The script detects existing headers and **does not** add duplicates. Any existing top-of-file comment counts as a header and will prevent insertion.

---

## 🛡 License

This project is licensed under the **GNU General Public License v3.0 or later**.
See the `COPYING` file or [GNU licenses](https://www.gnu.org/licenses/) for more details.

---

## 👤 Developer

**Jonathan Miller**
📧 [dev@mokoconsulting.tech](mailto:dev@mokoconsulting.tech)
🌐 [https://mokoconsulting.tech](https://mokoconsulting.tech)

---

*Questions or improvements? Open an issue or propose a PR.*
