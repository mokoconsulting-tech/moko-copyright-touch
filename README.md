# moko-copyright-touch — README

## Overview
`moko-copyright-touch.ps1` is a PowerShell script that recursively scans through a project directory to insert or replace standardized copyright headers in source files.

## Features
- Supports file types: **php, js, html, md, css, xml**.
- Automatically chooses the correct comment style for each file type.
- Replaces any existing top-of-file comment block with the new standardized header.
- Respects `.gitignore` patterns and skips `.git` folders.
- Loads configuration defaults from JSON files.
- Optionally outputs modified files to a separate destination folder.
- Can persist the selected `StartIn` folder back to a JSON config with `-PersistStartIn`.

## Developer Information
**Author:** Jonathan Miller  
**Organization:** Moko Consulting  
**Email:** hello@mokoconsulting.tech  
**Phone:** ‪(931) 279-6313

## Configuration
The script reads parameters from a JSON file in this order:
1. `-StartIn` parameter from CLI or shortcut.
2. `moko-copyright-touch.json` in the **project root**.
3. `moko-copyright-touch.json` in the **script folder**.

If no JSON file is found in either location, the script prompts for parameters and:
- Saves them to a new JSON file in the **selected project root**.
- Also saves them to a JSON file in the **script folder** so future runs without a project JSON can use them as defaults.

### Default JSON Structure
Below is an example of how a default JSON file should be structured. This can be placed in the **script folder** so it is used as a fallback for all projects when no project-specific JSON is present.
```json
{
  "StartIn": "path/to/your/project",
  "Holder": "[Your Name] || [Your Organization]",
  "Email": "your-email@example.com",
  "Phone": "your-phone-number",
  "ProjectGroup": "Project",
  "ProjectName": "MyProject",
  "Version": "1.0.0",
  "Years": "2023-2025",
  "License": "GPL-3.0-or-later"
}
```

## Usage Examples
Run normally:
```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File "./moko-copyright-touch.ps1"
```
With a preselected start folder:
```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File "./moko-copyright-touch.ps1" -StartIn "D:\\Code\\MyProject"
```
Dry-run (no writes, verbose logging):
```powershell
pwsh -File ./moko-copyright-touch.ps1 -DryRun -VerboseLog
```
Persist StartIn back to project JSON:
```powershell
pwsh -File ./moko-copyright-touch.ps1 -PersistStartIn
```

## How Headers are Formatted
- **Block style** (`/* ... */`) for PHP, JS, CSS.
- **HTML/XML comment style** (`<!-- ... -->`) for HTML, XML, MD.
- Includes copyright line, contact info, project details, and license/warranty disclaimer.

## Notes
- Always uses PowerShell 7+ ternary operators.
- Requires `System.Windows.Forms` for folder selection dialogs.
- Writes JSON to both the project root and script folder when prompted for parameters on first run.
- Uses script-folder JSON as fallback defaults when no project JSON is found.
