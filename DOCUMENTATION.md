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

# Script Runtime Flags

| Flag / Parameter         | Description                                                                                   | Example Usage |
|--------------------------|-----------------------------------------------------------------------------------------------|--------------|
| `-StartIn`               | Path to the root folder to scan for files. Overrides the value in the params file.           | `-StartIn ./src` |
| `-ParamsPath`            | Path to a specific `moko-copyright-touch.params.json` file to load.                          | `-ParamsPath ./config/params.json` |
| `-NoPrompt`              | Disables prompting for missing values; script fails if required params are not set.          | `-NoPrompt` |
| `--ProjectName`          | Overrides `projectname` from params.                                                          | `--ProjectName MyProject` |
| `--License`              | Overrides `license` from params.                                                              | `--License MIT` |
| `--Template`             | Uses a specific header template from the `templates` directory.                              | `--Template gpl-block` |

---

# Parameters Documentation

Every parameter in `moko-copyright-touch.params.json` is **required**.  
If not present, the script will prompt for it and write the value to the params file.

| Parameter                  | Type                 | Default                                         | Description                                                                                                    | Example |
|----------------------------|----------------------|-------------------------------------------------|----------------------------------------------------------------------------------------------------------------|---------|
| `startin`                  | string               | *(none)*                                        | Absolute path to root scan directory.                                                                          | `/var/www/project` |
| `destination`              | string               | `startin`                                       | Output path for modified files or backups.                                                                     | `/var/www/project/output` |
| `holder`                   | string               | `""`                                            | Copyright holder in the format `Name || Organization`.                                                         | `Jonathan Miller || Moko Consulting` |
| `email`                    | string               | `""`                                            | Contact email for the copyright holder.                                                                        | `hello@mokoconsulting.tech` |
| `phone`                    | string               | `""`                                            | Contact phone number.                                                                                          | `+1-931-431-8110` |
| `years`                    | string               | current year                                    | Year or range for copyright.                                                                                   | `2023-2025` |
| `license`                  | string               | `GPL-3.0-or-later`                              | SPDX license identifier.                                                                                       | `MIT` |
| `additonalinfo`             | boolean or string    | `false`                                         | Extra warranty/disclaimer text.                                                                                | `This software is provided as-is.` |
| `wordwrap`                  | integer              | `40`                                            | Max characters before wrapping text.                                                                           | `60` |
| `includesubdirectories`     | boolean              | `true`                                          | Whether subdirectories are scanned.                                                                            | `false` |
| `filetypes`                 | array[string]        | [".php", ".js", ".css", ".html", ".ini", ".xml"]| File extensions to process.                                                                                    | `[".php", ".md"]` |
| `ignorepatterns`            | array[string]        | See defaults                                    | Patterns to skip (supports wildcards).                                                                         | `["vendor", "*.min.js"]` |
| `backupbeforemodify`        | boolean              | `true`                                          | Whether backups are created before file changes.                                                               | `false` |
| `backuplocation`            | string               | `./.moko-copyright-touch-backups`               | Where backups are stored (relative to `startin`).                                                              | `./backups` |
| `headertemplate`            | string               | `""`                                            | Name of header template file. Must be valid JSON with escaped newlines. See **Header Template Documentation**. | `moko-copyright-touch.headertemplate.json` |
| `defaultdefgroup`           | string               | `Dolibarr`                                      | Default `@defgroup` value for Doxygen.                                                                          | `MyGroup` |
| `defaultingroup`            | string               | `Template.moko-cassiopeia`                      | Default `@ingroup` value for Doxygen.                                                                           | `MyTemplate` |
| `relativefilepathinheader`  | boolean              | `true`                                          | Include relative file path in `@file` tag.                                                                     | `false` |
| `promptformissingvalues`    | boolean              | `true`                                          | Whether to prompt for missing parameters.                                                                      | `false` |

---

# Header Template Documentation

The `headertemplate` variable points to a JSON file mapping file extensions to header formats.  

## JSON Formatting Rules
- Keys = file extensions without the dot (e.g., `"php"`, `"html"`).
- Values = JSON strings with **escaped newlines** (`\n`).
- Placeholders are wrapped in double curly braces: `{{Placeholder}}`.
- If no template exists for a file type, the `php` template is used.

## Supported Placeholders
`{{years}}`, `{{holder}}`, `{{email}}`, `{{phone}}`, `{{license}}`,  
`{{defgroup}}`, `{{brief}}`, `{{filename}}`, `{{ingroup}}`, `{{description}}`,  
`{{projectname}}`, `{{additionalinfo}}`

---

## Example: PHP Template with All Placeholders
```json
"php": "/*\\n * Copyright (C) {{years}} {{holder}} <{{email}}> {{phone}}\\n * Licensed under {{license}}\\n *\\n * Project: {{projectname}}\\n *\\n * {{additionalinfo}}\\n */\\n\\n/**\\n * @defgroup    {{defgroup}}\\n * @brief       {{brief}}\\n * @file        {{filename}}\\n * @ingroup     {{ingroup}}\\n * @description {{description}}\\n */"
