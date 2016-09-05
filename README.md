Drupal registry rebuild script. 
Original script from https://www.drupal.org/project/registry_rebuild

THIS IS NOT A MODULE. YOU CAN'T ENABLE IT. FOLLOW THE INSTRUCTIONS.

When would you need Registry Rebuild?

You might get something like:

PHP Fatal error:  Class 'EntityAPIControllerExportable' not found in ...sites/all/modules/rules/includes/rules.core.inc on line 11

If this happens when you're trying to run update.php, and happens when you're trying to clear your cache, well, you have some trouble. That's what Registry Rebuild is for.

It also may happen that you've moved some module that Drupal requires to bootstrap, and you get a horrible error. Registry Rebuild will also rebuild the system table to get the modules in the right place so you can bootstrap.
When would you *not* need Registry Rebuild?

If you can access any page, or install a module, or run update.php, you almost certainly don't need Registry Rebuild.

Drush usage is preferred and best maintained. You probably *can* use registry_rebuild without drush. See below.

How To Use Registry Rebuild Without Drush

This isn't a module, but it's just packaged as a module download to make it so
it's easy to find and people can download it as a package.

    Make a backup of your database using any technique you like. drush sql-dump >dump.sql or mysqldump -uuser -ppassword dbname >dump.sql or use phpMyAdmin or whatever. I know of no way that this procedure can harm your database, but on the other hand if it doesn't work, you can get me the database and I can improve the module to deal with your situation.
    Make a directory for the php file, probably sites/all/modules/registry_rebuild (or for a multisite, sites/mymultisite/modules/registry_rebuild.
    *If* your modules are not in sites/all/modules, you will probably have to edit registry_rebuild.php to set DRUPAL_ROOT to what it should be.
    Copy the registry_rebuild.php from the package into that directory.
    You don't need to enable it. If you were able to enable it it means you didn't actually need it.
    Either run it from the command line:

       cd sites/all/modules/registry_rebuild
       php registry_rebuild.php

    OR
    point your web browser to
    http://example.com/sites/all/modules/registry_rebuild/registry_rebuild.php
    Changing "example.com" to your own site's base URL of course.
    You should see something like this:

    DRUPAL_ROOT is /home/rfay/workspace/commerce.
    There were 631 files in the registry before and 508 files now.
    If you don't see any crazy fatal errors, your registry has been rebuilt. You will probably want to flush your caches now.

    Hopefully you'll now be able to go about your affairs in peace, updating, clearing cache, etc.

This package comes with no guarantee explicit or implicit.

There's no reason it should do any harm to your install. But there can be lots of things wrong with a system, and the registry problem is not the fix for everything.

For multisite installations: Use the drush version and use it from sites/yourbrokensite. It should work fine.