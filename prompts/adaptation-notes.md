# Adaptation Notes

Copy `files/script.php` and edit the copy in place. Keep the service provider, the installer lifecycle callbacks, the compatibility checks and the WebTolk post-install layout. Use the steps below as the scope of a standard adaptation.

## Confirm optional installer actions

Check the target extension's manifest, existing installer hooks and package or build steps for anything that already manages plugin activation or Joomla layouts.

Ask the user both questions before adding or connecting either action to this script.

1. Should this installer automatically enable the target plugin?
2. Should this installer install, update and remove the Joomla layouts?

State where you found any existing implementation. For a plugin, propose automatic activation on first installation. For an extension with shared Joomla layouts, check who installs them and propose the installer script when it needs to own those files. Wait for an explicit answer to each question and add only the actions the user assigns to this script.

## Joomla 5 and 6 API

Resolve `joomla.core.source.5` or `joomla.core.source.6` through ProcessForge for the versions the target extension supports. Check the API used by the adapted script against each supported branch. Exclude classes, methods and aliases marked `@deprecated`.

Use `Joomla\CMS\Installer\InstallerScriptInterface` and `Joomla\CMS\Installer\InstallerAdapter` for installer hooks. For layout filesystem operations, use `Joomla\Filesystem\File`, `Joomla\Filesystem\Folder` and `Joomla\Filesystem\Path`. For a new database dependency, obtain `Joomla\Database\DatabaseInterface` from the container.

## Apply the template

1. Copy the PHP file into the target extension and reference it in the Joomla manifest's `<scriptfile>` element. If the element already exists, use its current path.
2. Copy both files from each locale directory and adapt their names and keys as described under [Language files](#language-files).
3. Update the package metadata, language text and any extension-specific links. Apply the [version tag rules](#version-tags) to the PHP docblocks. Keep the WebTolk logo, website and community links for a WebTolk-branded installer.
4. Set `$minimumJoomla` and `$minimumPhp` to the requirements of the target Joomla 5 or 6 extension. Keep the existing compatibility check logic.
5. For confirmed auto-enablement, set `$plugin->element` and `$plugin->folder` in `enablePlugin()` to the target plugin's element and group. Apply automatic activation on first installation by default and preserve the administrator's choice on updates. When the user declines automatic activation in this script, remove the call, the method and any database setup used exclusively by it.
6. For confirmed layout management, use the target manifest's `<layouts>` section to identify package files and their destination under Joomla's shared `layouts` directory. Copy the listed entries on installation and updates, and remove the listed entries on uninstall. Check that each path stays inside the layout directory owned by the extension.
7. Compare the result with `files/script.php` and check that every change serves the target extension. Verify the `.sys.ini` files in both locales define every key the installer reads. Check for unresolved placeholders and donor identifiers, then run `php -l` on the adapted script.

## Version tags

- Keep `@version __DEPLOY_VERSION__` in source docblocks. At release packaging, the build tool, such as Phing Packager, writes the extension's release version into `@version`.
- Use `@since __SINCE_VERSION__` in the reusable template. Resolve it to the version that introduced the code when adapting or through an explicit build rule for that token. Preserve an existing introduction version when adapting existing code.
- Phing Packager's regular build handles `__DEPLOY_VERSION__`. For a project that uses the separate `reset-since` command, set `replace.sinceResetToken` to `__SINCE_VERSION__` for deliberate resets.

## Language files

- Copy the `.ini` and `.sys.ini` templates for both `en-GB` and `ru-RU`. Put translations used by the installed extension in `.ini`. Keep installer messages and the manifest's name and description in `.sys.ini`.
- Replace `{TYPE}_{group}_{element}` in filenames with the lower-case language basename expected by Joomla. For a plugin, take the group and element from the target manifest, such as `plg_system_example`. For an extension without a group, omit that segment and its separator, as in `com_example`, `mod_example` or `pkg_example`.
- Replace the prefix in all language keys and in `LANGUAGE_PREFIX` in `script.php` with the uppercase basename, such as `PLG_SYSTEM_EXAMPLE`. Keep the key suffixes and replace `{extension_name}` and `{extension_description}` with localized text. Fill `_WHATS_NEW` when the extension has release notes.
- Include both renamed files for each locale using the target manifest's existing language installation convention.

### Optional installer footer

Set `_FOOTER` in the `.sys.ini` files for links or notes shown immediately after `_WHATS_NEW` on installation and updates. Leave the value empty when the extension has no footer.

For a plugin, use a relative link to the administrator plugin list. Set `filter[element]` to the plugin element and `filter[folder]` to its group. Translate the link label in each locale. [WebTolk guide to Joomla administrator filters](https://web-tolk.ru/blog/joomla-ssylki-na-spiski-sushchnostej-s-filtratsiej)

```ini
PLG_SYSTEM_EXAMPLE_FOOTER="<p><a href=\"index.php?option=com_plugins&amp;view=plugins&amp;filter[element]=example&amp;filter[folder]=system\">Open plugin settings</a></p>"
```
