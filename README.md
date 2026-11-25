# WebTolk Joomla Installer Script for ProcessForge

This ProcessForge template package contains the WebTolk-branded Joomla installer script and its language files.

[Installer script](files/script.php) · [WebTolk](https://web-tolk.ru/) · [Process Forge](https://processforge.ru/)

Copy and adapt the installer script and matching language examples for Joomla extension packages. The included WT Max and AmoCRM RadicalForm strings are donor examples and must be retargeted unless the target package really uses them.

## Required Adaptation

- Replace extension identifiers, language keys, minimum Joomla/PHP versions, URLs, and visible product text.
- Remove or retarget plugin enablement logic when it does not apply to the target package.
- Search for donor identifiers before committing.

## ProcessForge releases

The package ID is `joomla-installer-script`. Each [release](https://github.com/WebTolk/pf-template-webtolk-joomla-installer-script/releases) includes a ZIP with `template.yaml` at its root. Extract it into the `joomla-installer-script` directory under your workplace reusable template root and register `template.yaml` in the workplace template registry.

ProcessForge reads the update source declared in `template.yaml`. See [CHANGELOG.md](CHANGELOG.md) for release changes.

The template is distributed under the [GNU General Public License v3.0](LICENSE).
