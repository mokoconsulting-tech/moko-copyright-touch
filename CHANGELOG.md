# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),  
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]
### Added
- Initial draft of `CHANGELOG.md`.
- Planned support for additional comment styles (e.g., shell script, SQL).
- Pending feature: Per-folder `headertemplate` overrides.

---

## [1.0.0] - 2025-08-13
### Added
- First public release of **moko-copyright-touch**.
- JSON-based parameter and header template system.
- Multi-language comment style support (`block`, `line`, `html`).
- Detection and updating of existing headers with project-specific markers.
- CLI parameter overrides for all settings.
- Interactive prompting for missing configuration values.
- Backup system before modifying files.
- Relative file path insertion in headers.
- Default `@defgroup` set to `Dolibarr`.
- Support for grouped file extensions in header templates.
- Documentation: `DOCUMENTATION.md`, `README.md`.
- Example templates for PHP and HTML.

### Changed
- Unified default `@defgroup` and `@ingroup` naming conventions.
- Improved file type detection and template fallback to `php`.

### Fixed
- Corrected block comment alignment for all supported languages.
- Fixed detection of shebang lines before header insertion.

---

## [0.1.0] - 2025-08-01
### Added
- Proof-of-concept script to apply static headers to PHP files.
- Basic parameter configuration via JSON.

[Unreleased]: https://github.com/mokoconsulting-tech/moko-copyright-touch/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/mokoconsulting-tech/moko-copyright-touch/releases/tag/v1.0.0
[0.1.0]: https://github.com/mokoconsulting-tech/moko-copyright-touch/releases/tag/v0.1.0
