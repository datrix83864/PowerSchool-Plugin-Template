# 📦 PowerSchool Plugin Naming & Referencing Guidelines

_Updated: 2025-06-26_

This document defines the best practices for naming, structuring, and referencing files in this PowerSchool plugin project. These standards ensure consistency, compatibility with PowerSchool’s plugin system, and ease of maintenance.

Updated guidance for the latest PowerSchool plugin development practices and a template to copy is found on the [GitHub PowerSchool Plugin Template](https://github.com/datrix83864/PowerSchool-Plugin-Template)

---

## 📁 Repository Naming

- Use **PascalCase** for your GitHub repository (e.g., `SchoologyPowerSync`).
- This name is automatically used for:
  - The internal plugin folder structure
  - The plugin `.zip` filename
  - Displayed labels inside PowerSchool (if dynamically injected)

---

## 🗂 Plugin ZIP Structure

The plugin build process generates a `.zip` with the following structure:

```html
SchoologyPowerSync/ ← Matches repo name
├── plugin.xml
├── web_root/
│ └── admin/
│ | |── schoology/
│ | |── schoology_api_settings.html
├── pagecataloging/
│ └── pages.json
├── MessageKeys/ ← Optional
│ └── en.properties
```

---

## 🔧 plugin.xml

- Use a placeholder (`__VERSION__`) for the version field.
- The build system replaces this with a numeric version from the GitHub tag (e.g. `0.1.0`).

```xml
<plugin xmlns="http://plugin.powerschool.pearson.com"
        name="Name your plugin here"
        version="__VERSION__"
        description="Describe your plugin here.">
</plugin>
```

## 📄 pages.json (pagecataloging)

Must be named pages.json (not page_definitions.json)

Must use a numeric version string (e.g., 0.1.0)

Do not use "admin" as a contextType

Example:

```json
{
  "pages": [
    {
      "htmlID": "navAdminSchoologySettings",
      "title": "Schoology API Settings",
      "version": "__VERSION__",
      "contextType": "main",
      "requiredContext": "none",
      "sortOrder": 100,
      "parentHTMLID": "navAdminCustomization",
      "pageURL": "/admin/schoology/schoology_api_settings.html"
    }
  ]
}
```

## 🔃 GitHub Automation

The GitHub Action pipeline:

Extracts the repository name and version tag

Replaces `__VERSION__` in plugin.xml and pages.json

Builds the plugin folder with the name of the repo

Zips the folder into:

```php-template
dist/<repo-name>-<version-tag>.zip
```

Example:

- Repo: SchoologyPowerSync
- Tag: v0.1.0-beta
- Outputs:
  - SchoologyPowerSync/ (plugin folder)
  - SchoologyPowerSync-0.1.0-beta.zip (final release file)
  - Injected version: 0.1.0

## 📛 Referencing HTML/CSS/JS

- All paths should be relative to web_root, not custom/
- Use .html extensions only (no .htm)
- Example URL:

```bash
/admin/schoology/schoology_api_settings.html
```

## 🔐 Page Security

- Use "contextType": "main" + "requiredContext": "none" for admin pages
- Place pages under /admin/ to inherit admin security
- Optionally add logic inside the page to verify user roles

## 🛑 Anti-Patterns to Avoid

|❌ Don’t Do This | ✅ Do This Instead |
|-----------------|--------------------|
| Use .htm extensions | Use .html everywhere|
| Hardcode version strings | Inject from tag during build |
| Use contextType: "admin" | Use contextType: "main" |
| Use WEB_ROOT/ uppercase | Use web_root/ lowercase for consistency |
| Reference custom/pages/ | Reference paths under web_root/ only |

## 🌐 Optional Enhancements

- Use MessageKeys/en.properties for i18n
- Add plugin version visibility inside the UI
- Include a CHANGELOG.md and auto-publish release notes

---

For questions or contributions, open an issue or PR in the repository.