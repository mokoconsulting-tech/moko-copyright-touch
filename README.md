# moko-copyright-touch — README

## Overview
`copyright-touch.ps1` is a PowerShell script that recursively scans through a project directory to insert or replace standardized copyright headers in source files.

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
**Phone:** (931) 279-6313

## Configuration
The script reads parameters from a JSON file in this order:
1. `-StartIn` parameter from CLI or shortcut.
2. `copyright-touch.json` in the **project root**.
3. `copyright-touch.json` in the **script folder**.

If no JSON file is found, the script prompts for parameters and saves them to a new JSON file in the selected project root.

### JSON Format Example
```json
{
  "StartIn": "J:/Shared drives/Development/Projects/MyProject",
  "Holder": "Jonathan Miller || Moko Consulting",
  "Email": "hello@mokoconsulting.tech",
  "Phone": "(931) 279-6313",
  "ProjectGroup": "Dolibarr",
  "ProjectName": "MyProject",
  "Version": "1.0.0",
  "Years": "2023-2025",
  "License": "GPL-3.0-or-later"
}
```

## Usage Examples
Run normally:
```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File "./copyright-touch.ps1"
```
With a preselected start folder:
```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File "./copyright-touch.ps1" -StartIn "D:\Code\MyProject"
```
Dry-run (no writes, verbose logging):
```powershell
pwsh -File ./copyright-touch.ps1 -DryRun -VerboseLog
```
Persist StartIn back to project JSON:
```powershell
pwsh -File ./copyright-touch.ps1 -PersistStartIn
```

## How Headers are Formatted
- **Block style** (`/* ... */`) for PHP, JS, CSS.
- **HTML/XML comment style** (`<!-- ... -->`) for HTML, XML, MD.
- Includes copyright line, contact info, project details, and license/warranty disclaimer.

## Notes
- Always uses PowerShell 7+ ternary operators.
- Requires `System.Windows.Forms` for folder selection dialogs.
- Writes JSON only when prompted for parameters or `-PersistStartIn` is used.
