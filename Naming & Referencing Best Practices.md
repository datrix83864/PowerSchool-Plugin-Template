# Naming & Referencing Best Practices for PowerSchool Plugins

---

## Overview

PowerSchool merges **all plugins’ `/custom/` folders into one global `/custom/` directory** on the server. This means:

- Your plugin’s files share the same `/custom/` URL root as other plugins and manual customizations.
- To avoid conflicts, **use unique folder and file names** within your plugin.
- Always reference assets and pages with root-relative URLs starting with `/custom/`.

---

## 1. Folder Structure and Namespacing

Structure your plugin’s `custom` folder with a **unique namespace folder** to prevent collisions.

### Recommended structure:

```html
/custom
    /pages
        /admin
            yourplugin_dashboard.html
    /web_root
        /yourpluginname
            /scripts
                main.js
            /styles
                style.css
            /images
                logo.png
```

---

## 2. Referencing Assets in Custom Pages

Use root-relative URLs starting with `/custom/` and include your namespace folder.

### Examples:

```html
<!-- Reference CSS -->
<link rel="stylesheet" href="/custom/web_root/yourpluginname/styles/style.css" />

<!-- Reference JavaScript -->
<script src="/custom/web_root/yourpluginname/scripts/main.js" defer></script>

<!-- Reference Images -->
<img src="/custom/web_root/yourpluginname/images/logo.png" alt="Logo" />
```

## 3. Referencing Custom Pages

Your pages live under /custom/pages/ after deployment.

Use unique file and folder names to avoid conflicts.

Access pages by URLs like:

`/custom/pages/admin/yourplugin_dashboard.html`

## 4. Why Not Rename /custom/?

The /custom/ path is a PowerSchool convention and shared namespace.

Renaming it in URLs will break asset loading.

Instead, use namespaced folders inside /custom/ for your plugin.

## 5. Best Practices Summary

| Practice                                                         | Reason                                      |
| ---------------------------------------------------------------- | ------------------------------------------- |
| Use a unique namespace folder inside `/custom/web_root/`         | Prevents asset conflicts with other plugins |
| Reference assets with root-relative URLs starting `/custom/`     | Ensures paths work across all environments  |
| Use unique names for custom pages                                | Avoids page filename collisions             |
| Include `defer` in script tags or place scripts before `</body>` | Improves page load performance              |
| Avoid hardcoding domains or environment-specific URLs            | Makes plugin portable and easier to deploy  |

## 6. Example Custom Page Snippet

```html
<html>
  <head>
    <title>Your Plugin Dashboard</title>
    <link rel="stylesheet" href="/custom/web_root/yourpluginname/styles/style.css" />
    <script src="/custom/web_root/yourpluginname/scripts/main.js" defer></script>
  </head>
  <body>
    <h1>Welcome to Your Plugin Dashboard</h1>
    <img src="/custom/web_root/yourpluginname/images/logo.png" alt="Plugin Logo" />
  </body>
</html>
```