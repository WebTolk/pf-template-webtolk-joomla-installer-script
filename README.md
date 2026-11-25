# WebTolk Joomla Installer Script for ProcessForge

This ProcessForge template package contains the WebTolk-branded Joomla installer script and its language files.

[Installer script](files/script.php) · [WebTolk](https://web-tolk.ru/) · [Process Forge](https://processforge.ru/)

## Adapt the template

Copy `files/script.php` to the path declared in the target Joomla manifest and edit that copy in place. Preserve the installer lifecycle, compatibility checks and WebTolk-branded layout. Limit changes to the extension's metadata, language keys, text and links, version requirements and installer actions confirmed by the user.

Target Joomla 5 and 6 and use supported APIs verified against the ProcessForge Joomla sources. Ask the user separately about automatic plugin activation and layout management before connecting either action.

Use the `en-GB` and `ru-RU` `pkg_lib_wtmax.sys.ini` files as the matching language pair. The AmoCRM RadicalForm INI files are reference examples for that plugin. [Adaptation steps](prompts/adaptation-notes.md)

## ProcessForge releases

The package ID is `joomla-installer-script`. Each [release](https://github.com/WebTolk/pf-template-webtolk-joomla-installer-script/releases) includes a ZIP with `template.yaml` at its root. Extract it into the `joomla-installer-script` directory under your workplace reusable template root and register `template.yaml` in the workplace template registry.

ProcessForge reads the update source declared in `template.yaml`. See [CHANGELOG.md](CHANGELOG.md) for release changes.

The template is distributed under the [GNU General Public License v3.0](LICENSE).
