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
2. Copy the `en-GB` and `ru-RU` `pkg_lib_wtmax.sys.ini` files from `files/language/`. Rename them for the target Joomla element and use the same language-key prefix in the PHP file and both INI files. The AmoCRM RadicalForm INI files are reference examples for that plugin.
3. Update the package metadata, language text and any extension-specific links. Keep the existing version placeholder when the target build supplies it. Keep the WebTolk logo, website and community links for a WebTolk-branded installer.
4. Set `$minimumJoomla` and `$minimumPhp` to the requirements of the target Joomla 5 or 6 extension. Keep the existing compatibility check logic.
5. For confirmed auto-enablement, set `$plugin->element` and `$plugin->folder` in `enablePlugin()` to the target plugin's element and group. Apply automatic activation on first installation by default and preserve the administrator's choice on updates. When the user declines automatic activation in this script, remove the call, the method and any database setup used exclusively by it.
6. For confirmed layout management, use the target manifest's `<layouts>` section to identify package files and their destination under Joomla's shared `layouts` directory. Copy the listed entries on installation and updates, and remove the listed entries on uninstall. Check that each path stays inside the layout directory owned by the extension.
7. Compare the result with `files/script.php` and check that every change serves the target extension. Verify both INI files define the keys the script reads, check for leftover donor identifiers and run `php -l` on the adapted script.
