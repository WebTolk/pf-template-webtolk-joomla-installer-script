# WebTolk Joomla Installer Script for ProcessForge

This ProcessForge template package contains the WebTolk-branded Joomla installer script and its language files.

[Installer script](files/script.php) · [WebTolk](https://web-tolk.ru/) · [Process Forge](https://processforge.ru/)

## Adapt the template

Copy `files/script.php` to the path declared in the target Joomla manifest and edit that copy in place. Preserve the installer lifecycle, compatibility checks and WebTolk-branded layout. Limit changes to the extension's metadata, language keys, text and links, version requirements and installer actions confirmed by the user.

Target Joomla 5 and 6 and use supported APIs verified against the ProcessForge Joomla sources. Ask the user separately about automatic plugin activation and layout management before connecting either action.

Keep `@version __DEPLOY_VERSION__` in PHP docblocks for build-time release version substitution. The template uses `@since __SINCE_VERSION__` for the version that introduced the code. [Version tag rules](prompts/adaptation-notes.md#version-tags)

Copy both language files for each locale. `{TYPE}_{group}_{element}.ini` contains runtime strings and `{TYPE}_{group}_{element}.sys.ini` contains installer messages and manifest strings. Rename them to match the extension, such as `plg_system_example.ini` and `plg_system_example.sys.ini` for a plugin. [Adaptation steps](prompts/adaptation-notes.md)

## ProcessForge releases

The package ID is `joomla-installer-script`. Each [release](https://github.com/WebTolk/pf-template-webtolk-joomla-installer-script/releases) includes a ZIP with `template.yaml` at its root. Extract it into the `joomla-installer-script` directory under your workplace reusable template root and register `template.yaml` in the workplace template registry.

ProcessForge reads the update source declared in `template.yaml`. See [CHANGELOG.md](CHANGELOG.md) for release changes.

The template is distributed under the [GNU General Public License v3.0](LICENSE).
