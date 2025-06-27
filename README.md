# Example PowerSchool Plugin Template

This repository contains a minimal PowerSchool plugin with a few sample custom pages.

## Repo Structure

- `plugin.xml`: Plugin metadata descriptor file
- `WEB_ROOT/admin/example_page.html`: Sample PowerSchool custom admin page
- `WEB_ROOT/guardian/example_page.html`: Sample PowerSchool custom admin page
- `WEB_ROOT/teachers/example_page.html`: Sample PowerSchool custom admin page
- `.github/workflows/build-plugin.yml`: GitHub Action that packages the plugin and attaches a ZIP to each GitHub release

## Usage

1. Edit or add your PowerSchool custom pages under `WEB_ROOT/`
2. Update `plugin.xml` metadata as needed. Note that the `version` attribute will match the version of your plugin if you use GitHub Actions.
3. Push changes to GitHub
4. Create a new GitHub release (e.g., tag `v1.0.0`)
5. The GitHub Action will create a ZIP plugin and attach it to the release
6. Download the ZIP from the release page and upload it via PowerSchool System > Plugin Management Configuration

---

Developed by Datrix83864
