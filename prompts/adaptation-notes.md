# Adaptation Notes

Copy `files/script.php` and edit the copy in place. Keep the service provider, the installer lifecycle callbacks, the compatibility checks and the WebTolk post-install layout. Use the steps below as the scope of a standard adaptation.

1. Copy the PHP file into the target extension and reference it in the Joomla manifest's `<scriptfile>` element. If the element already exists, use its current path.
2. Copy the `en-GB` and `ru-RU` `pkg_lib_wtmax.sys.ini` files from `files/language/`. Rename them for the target Joomla element and use the same language-key prefix in the PHP file and both INI files. The AmoCRM RadicalForm INI files are reference examples for that plugin.
3. Update the package metadata, language text and any extension-specific links. Keep the existing version placeholder when the target build supplies it. Keep the WebTolk logo, website and community links for a WebTolk-branded installer.
4. Adjust `$minimumJoomla` and `$minimumPhp` when the target extension requires different supported versions. Keep the existing compatibility check logic.
5. If the package should auto-enable an installed plugin, set `$plugin->element` and `$plugin->folder` in `enablePlugin()` to the target plugin's element and group. Otherwise, remove the call and method and any database setup used exclusively by that method.
6. Compare the result with `files/script.php` and check that every change serves the target extension. Verify both INI files define the keys the script reads, check for leftover donor identifiers and run `php -l` on the adapted script.
