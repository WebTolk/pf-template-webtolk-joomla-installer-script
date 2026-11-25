# WebTolk Joomla Installer Script for ProcessForge

This ProcessForge template package contains the WebTolk-branded Joomla installer script and its language files.

[Installer script](files/script.php) · [WebTolk](https://web-tolk.ru/) · [Process Forge](https://processforge.ru/)

## Adapt the template

Copy `files/script.php` to the path declared in the target Joomla manifest and edit that copy in place. Preserve the installer lifecycle, compatibility checks and WebTolk-branded layout. Limit changes to the extension's metadata, language keys, text and links, version requirements and installer actions confirmed by the user.

Target Joomla 5 and 6 and use supported APIs verified against the ProcessForge Joomla sources. Ask the user separately about automatic plugin activation and layout management before connecting either action.

Keep `@version __DEPLOY_VERSION__` in PHP docblocks for build-time release version substitution. The template uses `@since __SINCE_VERSION__` for the version that introduced the code. [Version tag rules](prompts/adaptation-notes.md#version-tags)

Copy both language files for each locale. `{TYPE}_{group}_{element}.ini` contains runtime strings and `{TYPE}_{group}_{element}.sys.ini` contains installer messages and manifest strings. Rename them to match the extension, such as `plg_system_example.ini` and `plg_system_example.sys.ini` for a plugin. [Adaptation steps](prompts/adaptation-notes.md)

For an optional block after What's new, use the `_FOOTER` key in the installer language files. [Footer example](prompts/adaptation-notes.md#optional-installer-footer)

## Install into ProcessForge

The package ID is `joomla-installer-script` and its manifest type is `reusable_template`. Share the [latest stable release](https://github.com/WebTolk/pf-template-webtolk-joomla-installer-script/releases/latest) with the agent installing it.

1. Download the package ZIP and `update-manifest.json`. Select the version of the `joomla-installer-script` subject that matches the ZIP and verify the ZIP against its `sha256`.
2. Resolve the destination with `python "<pf-root>/bin/pf.py" path-resolve --workplace "<workplace>" --path '${PF_TEMPLATES}/joomla-installer-script'`. For a first installation, extract the ZIP there with `template.yaml` at the destination root. For an existing registered installation, use the ProcessForge update flow.
3. Merge the template entry into `<workplace>/registries/templates.yaml`. Reuse the existing root ID for `${PF_TEMPLATES}` or add a root for it. Set the entry's `path` to the extracted manifest's actual path relative to the workplace, using the local resolved path if the configured root is outside the workplace.

The following entries use the default workplace path. Keep the other registry entries when merging them.

```yaml
template_roots:
  - id: global
    label: Workplace reusable templates
    path: '${PF_TEMPLATES}'
    scope: workplace
    status: available
templates:
  - id: joomla-installer-script
    title: Joomla installer script template
    kind: scaffold
    root_id: global
    template_root: global
    path: reusable-templates/joomla-installer-script/template.yaml
    status: available
```

Verify template discovery and register its declared update source with ProcessForge.

```sh
python "<pf-root>/bin/pf.py" template-doctor --workplace "<workplace>" --template joomla-installer-script
python "<pf-root>/bin/pf.py" update entity-sources rebuild --workplace "<workplace>"
```

See [CHANGELOG.md](CHANGELOG.md) for release changes.

The template is distributed under the [GNU General Public License v3.0](LICENSE).
